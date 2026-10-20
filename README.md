# Nickscan

Nickscan is a Windows desktop utility for checking username availability on
Telegram, Discord, and Minecraft Java Edition. It provides a local terminal
interface in English and Russian.

This repository contains the public project description. The application is
under development and is not currently distributed through this repository.

## Features

- Check usernames entered manually or loaded from a text file.
- Generate candidate usernames using length, character, and pattern settings.
- Save results locally, resume unfinished searches, and export CSV files.
- Pace requests and pause checks when a service imposes a cooldown.
- Keep an unconfirmed result separate from a confirmed available username.

The application checks names; it does not automatically register accounts,
claim usernames, or change an existing username.

## Minecraft Java Edition integration

Public profile lookup identifies existing player profiles. If no profile is
found, Nickscan marks the name as requiring confirmation; this alone does not
establish that the name can be selected.

Authenticated checks are intended to confirm selected names using Minecraft
Services. The Microsoft sign-in flow is implemented, including Xbox Live and
XSTS exchanges, Minecraft profile verification, and credential renewal.
Microsoft and Xbox sign-in have succeeded in live testing. Minecraft Services
currently rejects the authentication exchange with HTTP 403. Application access
is being investigated; successful end-to-end Minecraft sign-in and authenticated
name checks have not yet been verified with this application's client ID.

Requested access is for username availability checks by a signed-in Minecraft
Java Edition user. Nickscan is not a game launcher. Minecraft Bedrock Edition
gamertags are outside the current scope.

## Sign-in and local data

Microsoft sign-in uses device authorization. The user enters their password and
any additional verification on Microsoft's website. Nickscan requests
`XboxLive.signin` and `offline_access`.

Saved Microsoft refresh credentials and Minecraft access credentials are
encrypted using Windows DPAPI for the current Windows user. Removing the local
sign-in deletes the saved credential file. Microsoft application consent can
be revoked separately through the user's Microsoft account.

Search results and resumable queues are stored locally in SQLite. Exported CSV
files contain check results, not sign-in credentials.

## Service limits and limitations

The checker uses pacing, bounded retries, and shared cooldowns. It does not
guarantee a particular check rate or that a previously available name will
remain available. Authentication, licensing requirements, and service limits
still apply.

Telegram uses its authenticated API. Discord checks currently use a public
unauthenticated endpoint whose behavior and availability may change. Results
are specific to each platform and the time of the check.

## Project status

Nickscan is an independent project under active development. It is not affiliated
with or endorsed by Mojang, Microsoft, Telegram, or Discord.

For questions about the project, use this repository's Issues page.
