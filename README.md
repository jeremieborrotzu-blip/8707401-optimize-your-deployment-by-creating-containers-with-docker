# Libra - Share your documents securely!

> ⚠ **This is a dummy application**
>
> It was created to accompany the Docker course offered by OpenClassrooms. No security audit has been performed to validate its operation and as such it should under no circumstances be used in production.

## Getting Started With the Source Code

### Prerequisites

- [Go >= 1.23](https://go.dev/)
- [Make](https://www.gnu.org/software/make/)

### Commands

#### Build the application

```bash
make build
```

The generated binary will be available in the `./bin` directory. Run `./bin/libra -h` to see the available configuration options.

#### Generate the Docker images

```bash
make docker-images
```

The generated images will be named `libra/<variant>-latest`.

## License

[AGPL-3.0](./LICENCE)
