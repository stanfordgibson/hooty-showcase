# Architecture and system boundaries

## User and processing flow

AppSheet captures search requests in Google Sheets. A time-based Apps Script worker processes queued requests. The recorded status sequence is Queued → Resolving Address → Searching → Completed / Failed.

The workflow geocodes the destination, queries historical records in BigQuery, constructs summary outputs and calculates a deterministic assessment. The documented spreadsheet outputs include Crime Summary, Station Summary, Crime Time Summary, Safety Assessment and Safety Report. A Geocode Cache supports the geocoding workflow.

Police precinct polygons and station points support destination-to-precinct and nearest-station information. The conceptual diagram omits individual tables and operational endpoints intentionally.

## Assessment boundary

The assessment uses severity, frequency, station and temporal components. Prototype weighting alternatives were explored; this showcase does not claim that the weights are statistically validated or reveal the proprietary scoring implementation.

## Conversation boundary

The Ruby / Sinatra AI work shapes selected report data into context for Gemini. Its intended role is to explain results, discuss temporal context, provide available station information and clarify limitations. It must not compute new scores, override deterministic results or invent observations.

Recorded development work includes request identity checks, mock conversation tests and live Gemini integration. The exact current UI handoff between AppSheet and the Ruby conversation interface has not been reverified for this showcase.

## Geocoding and hosting

The project explored provider-agnostic geocoding using Pelias, Photon, Nominatim and Google. Do not interpret this as all providers being simultaneously deployed. Docker and Cloudflare are part of the recorded infrastructure work; their current deployment and recovery procedures need verification.

## Deliberately outside this showcase

Application source, credentials, infrastructure configuration, database exports, individual incident records and operational URLs are not included. The diagram describes responsibilities rather than exposing deployment topology.
