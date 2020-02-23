## Reqyt.run

{:toc}

### TLDR
```sh
 curl -d \
  '{"inputLanguage":"en", "outputLanguage":"nl", "text": "Could you translate this for me?"}' \
  -H "Content-Type: application/json" -X POST http://reqyt.run/google_translate
```
### What & Why
Where to start? What I'm trying to do here is to solve a certain issue. What is the issue? I'm trying to solve a certain problem for software developers.

Maybe I should start with what I think this is. I would say it's a market place for (micro?) services. So, what does that mean? Look at the internet nowadays. There are many small and big service providers for small data queries. For example:
- Google, could you show me all the matching websites for 'services marketplace'? And google will answer.
- Will it rain tomorrow in Amsterdam at 5?
- What was the average exchange rate of Bitcoin vs. the US dollar two weeks ago?
- Could you convert this image from to a 256x256 jpeg file?
- Please make a screenshot of how `https://nu.nl/` looks in Chrome.
- Send an email to 'mail@reqyt.run' with the following contents: ...

I can think of many more requests. So what is the problem here? Many service providers exist for these sort of thing. But what if you want to test them out quickly - or what if you want to integrate these services into your software? Typically, the flow is as follows:
- Setup account
- Connect credit card
- Get API key from website
- If lucky, there is a client library for your programming language
- Setup code
- Forward billing to the right place
- etc.

That's one side of the story. The other side of the story is what happens when you want something which doesn't exist yet. Maybe you'll do this:
- Develop the software (or find some open source base for what you need).
- Change it to a service (maybe as a Docker container?)
- Deploy it to some infrastructure (Kubernetes? ECS?) etc etc.

Next week, a colleague somewhere else wants to setup the same thing. So what happens? He/she will reinvent the wheel all over again.

So what can we do? I think an answer could be a marketplace for these sort of services. Reqyt.run is an attempt to setup something along these lines. So what do we do? We try to connect service providers and consumers in a simple way, e.g. a marketplace! I you made some nice service, it would be awesome if we lower the barrier of monetizing it! If you need a service, it would be nice to lower the barrier of trying out, using, and handling the cost administration.

### How?
Let's build a big registry for services. How? Let's say you've made some nice software to turn audio into annotated text. You provide this service at some internet (http) endpoint. You register your endpoint to the central registry, set a price for each request, and you'll be rich in no time :). I do think we need to take an extra step though and be really clear about the interfaces.

#### Interfaces
Many programming languages exist in the world today. Ideally the service you provide will be exported as part of a client library - giving users tools such as auto completion in their language of choice. We're really lucky though that the tools to do such things already exist! To name a few examples:
- Google protobuf
- Apache Thrift
- Corba
These tools allow you to define the interface using an IDL (interface description language), and then automatically generate server & client libraries for different languages, and the tools to send messages between the two. See for instance the `google_translate` [protobuf IDL](https://github.com/reqyt/reqyt/blob/master/functions/google_translate/interface.proto) from the introduction on this website.

#### Reqyt
How does reqyt.run work? The idea is to create wallets. Each request for information should use a wallet; credit is then transfered from the consumers wallet to the service providers wallet. The business model for reqyt.run is to take a small share from this to be able to sustain the platform.

### Future
Right now there is only a single public wallet that is used for all requests. The core API is almost finished which will allow creation of user accounts and associated wallets. Ofcourse money needs to be added to wallets to allow one to use it. Cryptocurrency could be a nice first step towards creating a profitable platform from reqyt. Scaling is also an issue, right now the platform runs on small VPS only :).

### Contributing
Yes, please! Very welcome! If you're interested feel free to contact me. I think reqyt.run is a super good idea, if you think so too or if you think it's a super bad idea - I would really like to know!

#### Open source
The source code is licensed under Apache 2.0; as such it's very open. Feel free to create a clone or whatever, but I would like to know what's going on if possible!

### Future

#### Decentralized
A decentralized variant of this concept might be possible using blockchains. I would really like to see one, but the speed of credit transfers might be too low.

#### Conflict
What if you're using a service that's supposed to show you a traffic map, but it suddenly decides to send you pictures of cats? The marketplace won't know. Maybe a voting system would help?

#### Tests
Run periodic tasks for endpoints.

### Thanks for reading!
