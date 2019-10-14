# PSW Refunds Web App Docker Configuration

Docker base configuration to create the neccesary containers to run the application
with an API, CMS and DB containers.

## Installation

Use [docker-compose](https://docs.docker.com/compose/) to build and run the containers.

```bash
docker-compose up -d
```

## Usage

```bash
docker-compose exec api <command>
docker-compose exec cms <command>
docker-compose exec db mysql -u -p
```

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.
