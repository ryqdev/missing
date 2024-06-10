

## Synchronous

The easiest way to make HTTP requests in Rust is with the reqwest crate:

```rust
use std::error::Error;

fn main() -> Result<(), Box<dyn Error>> {
    let resp = reqwest::blocking::get("https://httpbin.org/ip")?.text()?;
    println!("{:#?}", resp);
    Ok(())
}
```

In Cargo.toml:

```toml
[dependencies]
reqwest = { version = "0.11", features = ["blocking"] }
```

## Async

Reqwest also supports making asynchronous HTTP requests using Tokio:

```rust
use std::error::Error;

#[tokio::main]
async fn main() -> Result<(), Box<dyn Error>> {
    let resp = reqwest::get("https://httpbin.org/ip")
        .await?
        .text()
        .await?;
    println!("{:#?}", resp);
    Ok(())
}
```


In Cargo.toml:

```toml
[dependencies]
reqwest = "0.11"
tokio = { version = "1", features = ["full"] }

```

## Hyper

Reqwest is an easy to use wrapper around Hyper, which is a popular HTTP library for Rust. You can use it directly if you need more control over managing connections. A Hyper-based example is below and is largely inspired by an example in its documentation:

```rust
use hyper::{body::HttpBody as _, Client, Uri};
use std::error::Error;

#[tokio::main]
async fn main() -> Result<(), Box<dyn Error>> {
    let client = Client::new();

    let res = client
        .get(Uri::from_static("http://httpbin.org/ip"))
        .await?;

    println!("status: {}", res.status());

    let buf = hyper::body::to_bytes(res).await?;

    println!("body: {:?}", buf);
}
```

In Cargo.toml:

```toml
[dependencies]
hyper = { version = "0.14", features = ["full"] }
tokio = { version = "1", features = ["full"] }
```

