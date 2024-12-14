> [!Note]
> This project is still in the planning stage.

<div align = center>

<h1>Alym | عَلِيم</h1>

[![pre-commit.ci status](https://results.pre-commit.ci/badge/github/zefr0x/alym/main.svg)](https://results.pre-commit.ci/latest/github/zefr0x/alym/main)

A game changing, feature-rich, efficient, blazingly fast, highly extendable and easily integrated **news aggregation [deamon](<https://en.wikipedia.org/wiki/Daemon_(computing)>)** that aims to make the process of aggregating news more organized, light-weight, secure and private.

It's **not** just an RSS aggregator nor a feed reader, it's a `feed aggregator` which act as a middle man by accessing feeds from any source using `informants`, and communicating with `feed reeders` using [`D-Bus`](https://en.wikipedia.org/wiki/D-Bus) and [`Named Pipes`](https://en.wikipedia.org/wiki/Named_pipe) to display the news. It takes control of the database and it organizes everything so much that the feed reader's only job is to display the news.

What you wnat to read comes first, not the latest news.

---

[<kbd><br><b>Install</b><br><br></kbd>](#installation)
[<kbd><br><b>Contribute</b><br><br></kbd>](CONTRIBUTING.md)
[<kbd><br><b>Packaging</b><br><br></kbd>](PACKAGING.md)
[<kbd><br><b>Q&A</b><br><br></kbd>](#qa)

---

<br>

</div>

## Headline Features

- 🧾 Free software under the [AGPL-3.0](https://www.gnu.org/licenses/agpl-3.0.html) licence.
- 💪 Written in the [Rust](https://www.rust-lang.org/) programming language.
- ...

## Problems It Fix
1. Dispersion in strength:
   - There are many applications and libraries and each of them offers different advantages and disadvantages.
   - We aim to cover as many defects as possible while maintaining as many features as possible in one piece of software that everyone can use.
2. Unnecessary use of resources and non-modularity:
   - Most of the applications are accompanied by a graphical interface and a number of other things that are not considered essential within a news aggregator.
   - We aim to separate the news aggregator from the interface and from any other plugins and build them independently, to reduce resources and increase freedom to use different interfaces.
3. ...

## Concepts, Definitions and Ideas

1. `Informant`: The part that fetch feeds from there sources and convert them to a generic format that could be stored in the database.
   - They could be `Builtins` or `Extensions`.
   - Each one is responsable for dealing with specific protocol or type of feeds.
2. `Feed Aggregator`: It's what `Alym` is. It access feeds using `Informats`, store them in a database, and provides an [API](https://en.wikipedia.org/wiki/API) for `Feed Readers` to communicate with it and get contents.
   - It's the core of the oporation and we can have only one of it.
   - It should run all the time in the background.
   - For control or simple communication with `Feed Reader` it uses [`D-Bus`](https://en.wikipedia.org/wiki/D-Bus).
   - When we have a huge amount of data it will send them using [`Named Pipes`](https://en.wikipedia.org/wiki/Named_pipe) to `Feed Reader`.
   - The `D-Bus`/`Named Pipes` communication interface should be good for most use cases, but if not, it is moduler, so you can create another one rather then using it.
   - It is not usual for the user to interact with it directly.
   - It's not ment to be used for huge amount of users as a web service for example.
   - It can sync data between multiple devices (they can be servers running all the time) using a special syncing protocol and service that could be self-hosted.
   - It should support every feature a feed aggregator should have.
   - ...
3. `Feed Reader`: An application that display feeds and there contents to the user, by communicating with the `Feed Aggregator`.
   - They might also provide an interface to configure the `Feed Aggregator` and to manage feeds and everything related to them that the user might want to change. But no problem if this was a separate thing.
   - They are separate projects that just use the `Feed Aggregator`'s [API](https://en.wikipedia.org/wiki/API), there developers are able to build them as they like and users might select any one to use based on what they prefer.
   - It should not be running in the background.
   - It should not access the network by it self. It can only request the `Feed Agregator` for some extra media for a specific news or feed. The `Feed Aggregator` will take care of creating a secure and private request to obtain the extra media.
4. A notification/status interface might be implemented as part of the `Feed Reader` or as a completly separate project.
   - It ment to help saving time and resources by giving the user the summary so he don't need to open the whole `Feed Reader`.
   - It might be a desktop widget or a script that output some text to be displayed somewhare.
   - It should wait for a signal from the `Feed Aggregator` to update it's information.
5. Timers in the feed aggregator don't work by the user setting a time to fetch the data. The user will categorize every feed by it's importance and rate of posting news and any other influential factor to calculate a `number of interest/priority` that will determine how often data should be fetched from the source.
    - The feed aggregator will run a timer for every `number of priority` range, every feed falls in this range should be fetched ones in a random time before the timer ends and resets.
    - User should be able to specify ranges for the `number of priority`, and there maximum times that will be use in there timers. (This is a global setting, not for every feed)
    - This system will be used in every fetch related thing. If the user want to fetch all the feeds now, a very short maximum time will be used for every range tell they are reseted. And if the user want to fetch a single feed now, it will be poped from the timer's list.
    - If an error accured in the fetching process, it will not be poped from the timer's list so we can try again in a random time, but an error flag will be assigned to it, so the timer could be reseted without it beegin poped from it's list.
6. Network client
    - Every feed has it's own session.
    - Every feed has it's own proxy settings.
    - Tor integrations
       - Tor could be used for every feed, except i2p ones.
       - Tor works like a normal proxy, but every feed has an isolated circuit.
    - i2p integration
       - i2p feeds just work with i2p, no other choices (i2p is just fantastic).

## Installation

### AUR

Not available yet...

### From the git repository

> You need to have [`cargo`](https://doc.rust-lang.org/cargo/) installed in you system.

1. Clone the repository from github

```
git clone https://github.com/zefr0x/alym.git
```

2. Go to the directory

```
cd alym
```

3. Checkout to a release tag e.g. v1.0.0

```
git checkout vx.x.x
```

4. Use `cargo` to install it

```
cargo install --path=.
```

## Q&A

**Q:** Why?

- To improve the overall RSS clients experience and news aggregators in general on the Linux Desktop, since the existing clients usually use a lot of resources, don't support every feature a feed aggregator should have, and a lot of other disadvantages. Having a bad news aggregator might reduce our producivity and expose us to some privacy and security risks, which is contrary to the purpose of a news aggregator in the first place.

**Q:** What does `Alym'` mean?

- It is an Arabic word [`عَلِيم`](https://en.wiktionary.org/wiki/%D8%B9%D9%84%D9%8A%D9%85), means having great knowledge.
