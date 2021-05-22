# Freqtrade Hyperopt running in cloud example

## Quick example for optimizing an existing strategy and running in cloud

In this example we will take an existing strategy, [Strategy004](https://github.com/freqtrade/freqtrade-strategies/blob/master/user_data/strategies/Strategy004.py) and we will use Hyperopt Parameters to find more optimal settings with recent trading data. We will run our experiment in the cloud.

## Setting up Freqtrade on your local machine

In order to install and setup Freqtrade, I recommend following the instructions in the [Optimize trading strategy using Freqtrade](https://github.com/devbootstrap/optimize-trading-strategy-using-freqtrade) repo first.

## Run this demo

Assuming you have already installed freqtrade as shown above and are running using Docker, you can do the following to run this demo:

1. Clone this repo
1. Start Bot in Dry Run as a quick check