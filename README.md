# FacebookCyberSecurityCourseWeek7

# Project 7 - WordPress Pentesting

Time spent: **X** hours spent in total

> Objective: Find, analyze, recreate, and document **five vulnerabilities** affecting an old version of WordPress

## Pentesting Report

1.  Authenticated Stored Cross-Site Scripting (XSS) in YouTube URL Embeds
  - [ ] Summary: Contributors to the vulnerable site can embed a YouTube link with malicious XSS. This is due to a flaw in regex processing which allowed escape characters to initiate arbitrary code.
    - Vulnerability types: Core vulnerability, Stored XSS
    - Tested in version: 4.2
    - Fixed in version: 4.7.3
  - [ ] GIF Walkthrough:
    - ![Gif of 1](https://media.giphy.com/media/w8ZcgIokWUkAmTG9Lq/giphy.gif)
  - [ ] Steps to recreate: 
    - Copy an embedded youtube URL from any video.
    - Create embedded link for wordpress with pattern: ``` [embed src='https://www.youtube.com/embed/w0_QVQEbMas\x3csvg onload=alert(document.cookie)\x3e'][/embed] ```
    - Paste link into a post on wordpress page and publish.
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/4.9/src/wp-includes/embed.php#L227)
    - [Link 2](https://core.trac.wordpress.org/browser/tags/4.9/src/wp-includes/kses.php#L526)
    - [Link 3](https://core.trac.wordpress.org/browser/tags/4.9/src/wp-includes/class-wp-embed.php#L387)
    
1. Wordpress Does Not Invalidate Sessions Upon Logout CVE-2012-5868
  - [ ] Summary: WordPress 3.4.2 fails to invalidate a user’s sessions upon logout. When an administrator explicitly logs out of the admin interface, WordPress clears the client-side cookies, but doesn't invalidate the session id within the application. A malicious user could obtain someones previously authenticated user's session cookie and use it to gain access to the application.
    - Vulnerability types: User escalation, Session Hijacking, Authentication Bypass
    - Tested in version: 3.9
    - Fixed in version: 4.0
  - [ ] GIF Walkthrough: ![Gif of 2](https://media.giphy.com/media/RkDSrcJj3h6ZdCph5z/giphy.gif)
  - [ ] Steps to recreate: 
    - Capture cookies by examining GET request sent to http://wpdistillery.vm/wp-admin/profile.php
    - Log out of wordpress
    - Replay GET request using same cookies
    - Access is still permitted.
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/4.9/src/wp-includes/class-wp-session-tokens.php#L48)
1. (Required) Vulnerability Name or ID
  - [ ] Summary: It is possible to enumerate through author archives of wordpress. This can be performed automatically by the wpscan utility, but underneath involves sending requests to the site with different id values. Possible fixes involve firewall implementations and / or modifying the htaccess file with code like:
  ```
  # Block User ID Phishing Requests
<IfModule mod_rewrite.c>
	RewriteCond %{QUERY_STRING} ^author=([0-9]*) [NC]
	RewriteRule .* http://example.com/? [L,R=302]
</IfModule>
```
    - Vulnerability types: User Enumeration
    - Tested in version: 3.9
    - Fixed in version: ...
  - [ ] GIF Walkthrough: ![Gif of 3](https://media.giphy.com/media/mMEwgIz3SFq2wTE2PC/giphy.gif)
    - User Enumeration Manually: ![Gift of 4](https://media.giphy.com/media/4Z1OECCGHcfTk1Ds96/giphy.gif)
  - [ ] Steps to recreate: 
    - Using WPScan shell, enter command: ``` wpscan --url http://www,wordpressurl.com --enumerate u ```
    - Without proper safeguards, wpscan will output listing of names.
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/4.9/src/wp-includes/author-template.php#L401)

## Resources

- [WordPress Source Browser](https://core.trac.wordpress.org/browser/)
- [WordPress Developer Reference](https://developer.wordpress.org/reference/)

GIFs created with [LiceCap](http://www.cockos.com/licecap/).

## License

    Copyright [2018] [Jon Killinger]

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
