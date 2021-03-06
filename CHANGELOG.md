0.5.4
-----
- Added marker option to loads, so that load markers are optional
- OpenID client will now extract tokens from cookies as well as the header.

0.5.3
-----
- Added utility function integrate-ident!
- Refined merge-state!
- Renamed Constructor to InitialAppState
- Automated initialization of to-one unions (to-many was already doable by Om)

0.5.2
-----
- Fixed bug with initial state and new constructors

0.5.1
-----
- Added untangled/Constructor for adding initial state to UI components
- Added merge-state! for easily merging component-centric data (e.g. from server push)

0.5.0
------
- Significant optimizations to post-query processing.
- BREAKING CHANGE: to load-data. You should now include :refresh to trigger re-rendering of components. This removes the
  internal need for a forced root re-render. Proper refresh after load-data now requires this parameter.
- Removed deprecated load-collection and load-singleton. Use load-data instead (name change only)

0.4.9
-----
- Removed old logging code (use untangled.client.logging instead)
- Added support for parallel lazy loading
- Added `(start [this app])` to the `UntangledNetwork` protocol.
- Log-app-state now requires the atom containing a mounted untangled client, define it in the user namespace like so:
```
(defonce app (atom (uc/new-untangled-client ... )))
(swap! app uc/mount RootComponent "app-div")
(def log-app-state (partial util/log-app-state app))
```
- `global-error-callback` now expectes an arity 2 function. First param is the status and the second is the response.
- Fixed bug that closed over tempids in network callbacks
- Fixed bug in path-optimized union query parsing

0.4.8
-----
- Fixed tempid rewrite regression

0.4.7
-----
- Upgraded to Om-alpha32
- untangled.openid-client/setup, parses any openid claims from the webtoken in the url's hash fragments
- Renamed load-collection/singleton to load-data. Old names are deprecated, but not yet removed.
- Renamed :app/loading-data to :ui/loading-data
- Added remote trigger method for doing loading from mutations.
- Renamed everything in the internals that was prefixed app/ to untangled/
- Added global server error handler.
- Added fallback support for load-data, load-field, etc.
- Refactored networking send for better clarity
- Fixed bug on mark/sweep of missing query results. It was being applied to mutations instead of reads. Added tests for this that need a bit more work.

0.4.6
-----
- Fixed local read bug, and turned on path optimization
- Fixed fallback handling of failed remote transactions, and added lots of tests

0.4.5
-----
- Renamed react-key to ui/react-key
- Renamed app/locale to ui/locale
- Renamed mutation app/change-locale to ui/change-locale
- Implemented a number of missing things in i18n
- Removed a number of i18n helpers that were redundant to trf
- Added :request-transform networking hook with spec
- Modified load callback to a mutation symbol
- Changed :params of loaders to allow you to specify which prop on the query gets the stated parameters
- Added history method to application protocol, to make implementing history viewer in an app trivial

