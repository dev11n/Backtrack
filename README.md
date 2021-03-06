# « Back » Track «
A simple repository aimed at describing how to bypass several security-focused aspects of Star Stable Online
## Setup
1. Fiddler Everywhere
2. A basic understanding of how Fiddler works (trust the root certificate for HTTP/HTTPS connections, otherwise it won't work)
3. The game itself
4. A VPN is strongly recommended, either iVPN or MullvadVPN. No NordVPN or other bs like that which logs everything.
### Bypassing GameGuard (`2022-05-27`)
This is now obsolete, since GameGuard has been removed.
***
1. Launch Fiddler Everywhere
2. Trust the root certificate (`View » Preferences » HTTPS » Trust Root Certificate`)
3. Make sure the Fiddler port is set as `8866` (`View » Preferences » Connections`)
4. Add 3 new rules, here's a table of the information:

| Rule Name                        | Conditions                                                                                                                     | Actions                                                                          | Purpose                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|----------------------------------|--------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Fake Anti-Cheat Responses        | When `all these conditions` are met `any number of times` Url `Contains` `http://mgr.gameguard.co.kr/LogServer3/`              | `Update Url` `Append to value` `09`                                              | Appends a value to the URL of the request which should hinder it from gathering accurate enough results (at least from my testing).                                                                                                                                                                                                                                                                                                                                |
| Use a fake JSON to avoid patches | When `all these conditions` are met `any number of times` Url `Contains` `http://sso-released-prod.starstable.com/SSORelease`  | `Update Url` `Set value` `https://dont-play-sso.com/req/latest.json`             | Changes the URL the launcher uses to check for game files in order to stop it from trying to patch them. The external server does not have any game files to serve, this just acts like a dummy end-point.                                                                                                                                                                                                                                                         |
| Stop Driver Verification         | When `all these conditions` are met `specific number of times` `1` Url `Contains` `mgr.gameguard.co.kr/LogServer3/service.do?` | `Non Graceful Close` | This rule is only allowed to be executed once; Cancels (what seems to be like) a rather important web-request which hinders the driver from loading, leaving the memory exposed. |
5. Done.
