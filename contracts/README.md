# Dexterity smart contracts

Built with [foundry](https://github.com/foundry-rs/foundry).
Powered by `GNU make`.

## what is Dexterity?

It is a demonstration of architecture, security and invariants. It is not
intended to be used as-is in production.

### Security and design choices

#### why UniswapV2 and not V3 or V4?

Simplicity and understandability. Though v2 is not the most recent version,
it's still largely used and the architecture is easy to understand (each pool
is a pair of token and liquidity, hold in a mapping)

### What is not deliberately covered

- **Routes**: Users of `dexterity` must specify a specific `pair` to trade or
  deposit.
  For a real production project I would have implemented a **Router** contract
  exposing function to the user, facilitating trading using proper routing all
  along a token pair chain.
- **Trade**: as a mean for a user to easily `swap` their tokens. It would rely
  on `routes` and would require bound trading (see below).
  For a real production project, I would have implemented one user-facing
  functions to perform trade accordingly to a correct `route`.
- **Bound trades**: Actually, users can `swapIn` or `swapOut` for input or
  output token. However, not specifying a limit on resulting token amount, a
  front-running attack could drain users of their input swap for a zero output
  token amount.
  For a real production project, I would have bound swapIn and swapOut
  functions to ensure front running cannot drain input user token used for
  trading.

## setup

`make .env` to create all necessary environment variables.
Edit this file to set all values.
I repeat, edit this file to setup important variables.
If you do not it won't work.
Did I say you to edit this file to setup important variables?

## testing

### contracts

`make test` everything should be green.
`make coverage`: self-explanatory.
