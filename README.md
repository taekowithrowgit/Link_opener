# Link_opener

A personal fork of [crx-gcal-url-opener](https://github.com/Leko/crx-gcal-url-opener), not affiliated with or published on the Chrome Web Store listing of the original project.

This is a Chrome extension that automatically opens the URL set in your calendar event as a new tab a few minutes before the start of the Google Calendar event.

- **Easy to use**: Just log in with your Google account to link calendars and it's automatic.
- **Concentrate without worrying about time**: The tab will automatically open 1-2 minutes before the meeting. No more worrying about the time so you don't miss the MTG. You can focus on your task, not the clock.
- **Interrupt overconcentration**: Opens a new tab and brings that window to the forefront. You will never miss the MTG even if you are doing other tasks in a text editor, terminal, etc.
- Support Google Meet, Zoom, Microsoft Teams (beta), and Gather

## Getting started (personal build)

This fork is meant to be built and loaded locally as an unpacked extension, not published to the Chrome Web Store. It does not reuse the upstream project's Google OAuth client, so you need to create your own.

1. `npm i && npm run build` (creates the `dist` directory)
2. Go to `chrome://extensions`, enable "Developer mode", click "Load unpacked", and select the `dist` directory
3. Copy the extension ID shown on the card (a 32-character string)
4. In [Google Cloud Console](https://console.cloud.google.com/), create a project (or reuse one) and:
   - Enable the "Google Calendar API"
   - Configure the OAuth consent screen (External is fine; add your own Google account under "Test users" so you don't need Google's review)
   - Create an OAuth Client ID of type "Chrome Extension", using the extension ID from step 3
5. Put that client ID into `manifest.json`'s `oauth2.client_id` (replacing `YOUR_OAUTH_CLIENT_ID.apps.googleusercontent.com`), then `npm run build` again and click the reload icon for the extension on `chrome://extensions`
6. Click the popup icon and sign in with the Google account you added as a test user
7. You're all set! Events are automatically and regularly updated. You won't have to click the refresh button unless you want to retrieve the latest events immediately.

## Development

```
npm i
npm run dev
```

Then `dist` directory will be created on the project root. Please load it on `chrome://extensions`.

### Adding new video conference tools

1. Add a new element into `urlRules` in src/config.ts
2. Add tests in src/config.test.ts
3. Create a pull request

### Release

```
npm version {patch|minor|major}
npm run release
```

## License

This repository is under [MIT license](https://opensource.org/licenses/MIT).
