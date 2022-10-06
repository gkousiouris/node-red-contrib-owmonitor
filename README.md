node-red-contrib-owmonitor
=====================

This is a subflow node in order to monitor the latest performance (sliding window) of Openwhisk actions. The flow pings periodically the target Openwhisk installation in order to retrieve the last executed actions and extract statistics from their execution.

## Install

Run the following command in your Node-RED user directory - typically `~/.node-red`

        npm install node-red-contrib-owmonitor

## Information



This is a subflow node in order to monitor the latest performance (sliding window) of Openwhisk actions. The flow pings periodically the target Openwhisk installation in order to retrieve the last executed actions and extract statistics from their execution.

Configuration includes:
 - the polling time of the monitor (default 30 seconds, `msg.pollingPeriod`)
 - the target Openwhisk endpoint (`msg.targetEndpoint`)
 - credentials for that endpoint (`msg.creds`) in the form of user:key
 - the window of time (in minutes) in the past for which you want to retrieve results (`msg.window`)
 - an optional action name (`msg.action`), if one wants to filter specific action activations

The configuration can be set either via the flow UI or the incoming message. The incoming message prevails over the UI-set value.

The monitor can be stopped via a `msg.stop=true` message. The subflow uses a flow variable in order to control starting and stopping, hence only one OW monitor should be used in each flow.

The results include the raw data acquired (`msg.payload.rawData`) in the last window of time, as well as the moving averages of duration (`msg.payload.results.movingAverageDuration`), init time (`msg.payload.results.movingAverageInitTime`) and wait time (`msg.payload.results.movingAverageWaitTime`) of the window. The number of cold starts are also included (`msg.payload.results.coldStarts`) as well as the percentage with relation to the total calls (`msg.payload.results.coldStartPercentage`).



