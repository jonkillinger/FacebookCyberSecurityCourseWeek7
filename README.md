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
  - [ ] Summary: 
    - Vulnerability types:
    - Tested in version:
    - Fixed in version: 
  - [ ] GIF Walkthrough: 
  - [ ] Steps to recreate: 
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/version/src/source_file.php)
1. (Optional) Vulnerability Name or ID
  - [ ] Summary: 
    - Vulnerability types:
    - Tested in version:
    - Fixed in version: 
  - [ ] GIF Walkthrough: 
  - [ ] Steps to recreate: 
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/version/src/source_file.php)
1. (Optional) Vulnerability Name or ID
  - [ ] Summary: 
    - Vulnerability types:
    - Tested in version:
    - Fixed in version: 
  - [ ] GIF Walkthrough: 
  - [ ] Steps to recreate: 
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/version/src/source_file.php) 

## Assets

List any additional assets, such as scripts or files

## Resources

- [WordPress Source Browser](https://core.trac.wordpress.org/browser/)
- [WordPress Developer Reference](https://developer.wordpress.org/reference/)

GIFs created with [LiceCap](http://www.cockos.com/licecap/).

## Notes

Describe any challenges encountered while doing the work

## License

    Copyright [yyyy] [name of copyright owner]

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
