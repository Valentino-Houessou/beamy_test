## Guidelines

- Solve the levels in ascending order
- Only do one commit per level and include the `.git` when submiting your test

Please do the simplest thing that could work for the level you're currently solving.

We are interested in seeing code that is:

- Clean
- Extensible
- Reliable
- Dockerized

## Challenge

The challenge needs to be resolved in Typescript.
Each level depends on one Node v12.19 executable and one to many libraries that you'll have to use.
**You can't modify them.**
Your solution to each level needs to live in the `level{N}` directory.

## Level 1

Before everything, you'll need to do a `npm install`.
Launch the `npm run generate_logs` command.
It will write log messages into `./logs/#{id}.txt`.
Each file will contain one messsage log. The log looks like this:

```
id=0060cd38-9dd5-4eff-a72f-9705f3dd25d9 service_name=api process=api.233 sample#load_avg_1m=0.849 sample#load_avg_5m=0.561 sample#load_avg_15m=0.202
```

You need to write a program that will parse the messages, write the result to a JSON file in `./parsed/#{id}.json` and deletes the original message.
You need to write a JSON in the following format:

```
{
  "id": "2acc4f33-1f80-43d0-a4a6-b2d8c1dbbe47",
  "service_name": "web",
  "process": "web.1089",
  "load_avg_1m": "0.04",
  "load_avg_5m": "0.10",
  "load_avg_15m": "0.31"
}
```

## Level 2

When you launch the `npm run emit_logs` command it will send the same log messages to a local HTTP server at http://localhost:3000/ that you'll have to create.
The HTTP server listens to POST requests on the port 3000.

**The POST requests will timeout after 100ms.**

You need to write a simple HTTP server that will listen to this requests, parse the logs and write the result to a JSON file in `./parsed/#{id}.json` in the same format than Level 1.
To write a simple HTTP server look at [Express](https://expressjs.com/) or [Fastify](https://www.fastify.io/).

## Level 3

Launch the `npm run emit_logs` command.
This time your HTTP server need to parse the logs and send them to a Redis `LIST` on a local Redis instance (redis://localhost:6379).

## Level 4

Launch the `npm run emit_logs` command.
This time your HTTP server need to parse the logs and send them to a [MySQL](https://hub.docker.com/_/mysql) Table on a local MySQL instance. You'll need to create a data model with the 5 fields, and you can use TypeORM or Sequelize to create and save your entities.

## Level 5

Launch the `npm run emit_logs` command.
Your HTTP server, after parsing the logs, needs to enrich them with the library called `slow_computation`.

To understand how to use this library, you can look at the `exampleCompute.js` file.

As in level 4 you’ll save the resulting JSON in a SQL table.
**Again, the HTTP call will timeout after 100ms**.

---

We hope you'll have fun doing this challenge. It shouldn't take more than a few hours. Enjoy and be reliable <3
