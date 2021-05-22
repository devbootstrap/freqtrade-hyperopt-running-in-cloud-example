# Freqtrade Hyperopt running in cloud example

## Quick example for optimizing an existing strategy and running in cloud

In this example we will take an existing strategy, [Strategy004](https://github.com/freqtrade/freqtrade-strategies/blob/master/user_data/strategies/Strategy004.py) and we will use Hyperopt Parameters to find more optimal settings with recent trading data. We will run our experiment in the cloud.

## Setting up Freqtrade on your local machine

In order to install and setup Freqtrade, I recommend following the instructions in the [Optimize trading strategy using Freqtrade](https://github.com/devbootstrap/optimize-trading-strategy-using-freqtrade) repo first.

## Run this demo

Assuming you have already installed freqtrade as shown above and are running using Docker, you can do the following to run this demo:

1. Clone this repo
1. Start Bot in Dry Run as a quick check using `docker-compose up`and check the log output to confirm it is correctly using` Strategy004` and using the expected parameters.
1. Stop the Bot using `docker-compose down`
1. Run the hyperopt locally with just 2 epochs as a quick check that the Hyperopt is working
1. Start up a new instance, that has at least 4 CPU cores using the cloud provbider of your choice such as AWS, Digital Ocean or other
1. Install Docker and other dependencies on your new cloud instance
1. Run the bot hyperopt on the machine using 4000 epochs.

## How to setup from scratch

1. Download docker compose `curl https://raw.githubusercontent.com/freqtrade/freqtrade/stable/docker-compose.yml -o docker-compose.yml` and pull down the image `dc pull`
1. Run scaffold `dcr freqtrade create-userdir --userdir user_data`
1. Run config generator `dcr freqtrade new-config --config user_data/config.json`
1. Update config pairs with the pairs you want to use
1. Copy [Strategy004](https://github.com/freqtrade/freqtrade-strategies/blob/master/user_data/strategies/Strategy004.py) (or the strategy you want to use)
1. Update `docker-compose.yml` strategy using `--strategy Strategy004`
1. Run dry run check `docker-compose up`
1. Update the strategy with a few Hyperopt params to begin with so that you can test you have everything wired up.
1. Download Data for Hyperopt, for example 5m candles: `dcr freqtrade download-data --exchange binance -t 5m`
1. Run Hyperopt tool to check with just 2 epochs `dcr freqtrade hyperopt --hyperopt-loss SharpeHyperOptLoss --strategy Strategy004 -i 5m -e 2`
1. Deploy to cloud `git clone https://github.com/devbootstrap/freqtrade-hyperopt-running-in-cloud-example.git` (assumes cloud instance already setup with git, docker and so on installed).
  cd freqtrade-hyperopt-running-in-cloud-example/ft_userdata
1. Pull image onto the cloud instance `dc pull` (assumes you are in the correct directory and have aliased the command `dc` to `docker-compose`)
1. Run hyperopt 3000 (or more if you like) epochs `dcr freqtrade hyperopt --hyperopt-loss SharpeHyperOptLoss --strategy Strategy004 -i 5m -e 3000`
1. End hyperopt and update strategy with results by updating the default values in the strategy hyperopt params.
1. Run dry run again and maybe go live.