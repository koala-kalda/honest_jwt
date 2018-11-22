Honest JWT Library
==================

Implementation of [JSON Web Tokens](http://jwt.io) in Rust. Honest about its feature set and actively maintained. Support for all claim checks and JWEs is a goal. Fork of [frank_jwt](https://github.com/GildedHonour/frank_jwt).

## Algorithms and features supported
- [x] HS256
- [x] HS384
- [x] HS512
- [x] RS256
- [x] RS384
- [x] RS512
- [x] ES256
- [x] ES384
- [x] ES512
- [x] Sign
- [x] Verify
- [ ] iss check (issuer)
- [ ] sub check (subject)
- [ ] aud check (audience)
- [ ] exp check (expiration time)
- [ ] nbf check (not before time)
- [ ] iat check (issued at)
- [ ] jti check (JWT id)

## Usage

Put this into your `Cargo.toml`:

```toml
[dependencies]
honest_jwt = "0.1"
```

And this in your crate root:

```rust
extern crate honest_jwt;
extern crate  #[macro_use] serde_json;

use honest_jwt::{Algorithm, encode, decode};
```

## Example
```rust
//HS256
let mut payload = json!({
    "key1" : "val1",
    "key2" : "val2"
});
let mut header = json!({});
let secret = "secret123";
let jwt = encode(&header, secret.to_string(), &payload, Algorithm::HS256);

//RS256
use std::env;

let mut payload = json!({
    "key1" : "val1",
    "key2" : "val2"
});
let mut header = json!({});
let mut keypath = env::current_dir().unwrap();
keypath.push("some_folder");
keypath.push("my_rsa_2048_key.pem");
let jwt = encode(&header, &keypath.to_path_buf(), &payload, Algorithm::RS256);
let (header, payload) = decode(&jwt, &keypath.to_path_buf(), Algorithm::RS256);
```

## License
Original project code ([frank_jwt](https://github.com/GildedHonour/frank_jwt)) was licensed under the [Apache 2.0](legal/apache-v2.0.md) license. New code is being written under the [LGPL 3.0](legal/gnu-lgpl-v3.0.md). Eventually all original code will be re-rewitten and entire project will be LGPL'd.
