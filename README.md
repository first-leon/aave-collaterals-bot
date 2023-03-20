### AAVE collaterals monitoring bot

Prometheus expoter which parses borrowers data from AAVE protocol and calculate risks distribution
based on collateral to loan ratio.

#### Run

`docker compose`

- Create a `.env` file from `.env.example` and fill in the required variables.
- Execute command:
```bash
docker compose up -d bot
```

`docker`

- Create a `.env` file from `.env.example` and fill in the required variables.
- Build image:
```bash
docker build -t aave-bot .
```
- Run container:
```bash
docker run -d -P --env-file ./.env aave-bot
```

`dev`

- Expose environment variables presented at `.env.example`.
- Install dependencies via poetry:
``` bash
poetry install
```
- Execute command:
```bash
python src/main.py
```

#### Zones definition

Risk zones defined as a ranges of collateral to loan ration and can be found at `./src/bot/bins.py` file.

#### The most important exposed metrics

- `{}_collateral_percentage{pair=<pair>, zone=<zone>, bin=<bin>}` is computed percent of collaterals in the given pair,
zone and bin

#### Visualisation

Pre-built grafana dashboards available in the `./grafana` directory. To run locally use docker-compose file as a
reference.

## Release flow

To create new release:

1. Merge all changes to the `master` branch
1. Navigate to Repo => Actions
1. Run action "Prepare release" action against `master` branch
1. When action execution is finished, navigate to Repo => Pull requests
1. Find pull request named "chore(release): X.X.X" review and merge it with "Rebase and merge" (or "Squash and merge")
1. After merge release action will be triggered automatically
1. Navigate to Repo => Actions and see last actions logs for further details 
