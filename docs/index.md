# Getting Started

Welcome to Momento the worlds first serverless caching service. Momento unlocks innovation at scale by giving developers an easy to use cache that works without any of the operational overhead required by traditional caching solutions. It is quick to provision, easy to use, and gives customers consistent performance. Momento allows developers to focus on their business logic, while giving them rapid access to an easy-to-use cache that has decades of mission critical scale experience and hard learned lessons already baked in.


## Quick start

#### Install CLI
The quickest way to get started is with our CLI. To get going simply install from our home brew tap.

```
brew tap momentohq/tap
brew install momento-cli
```

To verify the CLI was installed correctly you can run our help command
```
$ momento --help
momento 0.12.8
CLI for Momento APIs

USAGE:
    momento [OPTIONS] <SUBCOMMAND>

OPTIONS:
    -h, --help       Print help information
    -V, --version    Print version information
        --verbose

SUBCOMMANDS:
    account      Manage Accounts
    cache        Cache Operations
    configure    Configure Momento Credentials
    help         Print this message or the help of the given subcommand(s)
```


### Obtain an auth token
Being a developer focused company you can sign up for an auth token to use Momentos APIs right from the command line. We are going to use the `account` command to obtain an API token for your desired region with the Momento CLI. 
```console
$ momento account signup --region us-west-2 --email your-email@example.com
```

You will be emailed the API token to use. You can configure your local cli to use this token by running the momento `configure` command.
```
$ momento configure
Token: // < Enter token from email here.
Default Cache [default-cache]: my-first-cache // Name of cache to use on CLI by default.
Default Ttl Seconds [600]: 30 // Sets the default TTL for cache entries. For demostration purposes we are setting this lower right now.
[2022-03-31T15:31:25Z INFO  momento::commands::cache::cache_cli] creating cache...
[2022-03-31T15:31:33Z INFO  momento::commands::configure::configure_cli] default cache successfully created
```

### Cache some data!

You are now up and running with Momento! Lets check out the `cache` command to see how we can interact with our new cache. 

Note: You can use `momento cache $SUBCOMMAND --help` on any CLI commands to learn more
```
$ momento cache --help
momento-cache
Cache Operations

USAGE:
    momento cache [OPTIONS] <SUBCOMMAND>

OPTIONS:
    -h, --help       Print help information
        --verbose

SUBCOMMANDS:
    create    Creates a Momento Cache
    delete    Deletes the cache
    get       Gets item from the cache
    help      Print this message or the help of the given subcommand(s)
    list      Lists all momento caches
    set       Stores a given item in cache
```

Let's perform a set / get operation. We will make sure that the item disappears after the TTL has elapsed.
```
$ momento cache set --key test --value value
[2022-03-31T15:45:17Z INFO  momento::commands::cache::cache_cli] setting key: test into cache: my-first-cache
[2022-03-31T15:45:18Z INFO  momento::commands::cache::cache_cli] set success
$ momento cache get --key test
[2022-03-31T15:45:25Z INFO  momento::commands::cache::cache_cli] getting key: test from cache: my-first-cache
value
$ sleep 30 // wait for item to expire
$ momento cache get --key test
[2022-03-31T15:46:02Z INFO  momento::commands::cache::cache_cli] getting key: test from cache: my-first-cache
[2022-03-31T15:46:03Z INFO  momento::commands::cache::cache_cli] cache miss
```

And thats it! You are now caching data with Momento! 🎉

## Next steps

Check out our SDKs! We currently have the following SDK's languages availabile. 

* [.NET](https://github.com/momentohq/client-sdk-examples/tree/main/dotnet)
* [Go](https://github.com/momentohq/client-sdk-examples/tree/main/golang)
* [Java](https://github.com/momentohq/client-sdk-examples/tree/main/java)
* [JavaScript](https://github.com/momentohq/client-sdk-examples/tree/main/javascript)
* [Python](https://github.com/momentohq/client-sdk-examples/tree/main/python)
* [CLI（MacOS/Linux](https://github.com/momentohq/momento-cli)

Also check out our [examples repo](https://github.com/momentohq/client-sdk-examples/) for hands on examples with the various sdks.