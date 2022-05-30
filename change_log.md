# Change log
## \#001: Adjust lane switching to multiple lanes
- kappa.size = number of red lanes at crossway
- toggle lane status must be adjusted that lanes becoming green are specified as green lanes
  * tlLogic --> junction id
  * junction --> internal lanes
  * connections: internal lanes --> incoming lanes
  * tlLogic.state + order of internal lanes + mapping of internal lanes and incoming lanes --> phases of incoming lanes by indices of 'G' or 'g'

## \#002: Decide lane switching in cases of conflicting lanes
- detect conflict and the corresponding lanes
- define rules to solve conflicts 