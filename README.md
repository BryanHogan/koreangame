# Game To Learn Korean

Make learning with flashcards more fun, and even more efficient.

## Tech-Stack
This project is built using the following technologies:
- Astro framework
- CapacitorJS: Export project as app to Android and iOS
- Tauri: Export project for Windows, Linux and mac
- TailwindCSS
- DiasyUI
- AstroJS/Svelte: Use Svelte components in Astro
- PostCSS & postcss-preset-env: CSS converter

## Steps to set up this project

- Install Astro: `npm create astro@latest` - https://docs.astro.build/en/install/auto/
- Install Svelte components integration for Astro: `npx astro add svelte` - https://docs.astro.build/en/guides/integrations-guide/svelte/
- Add Tailwind: `npx astro add tailwind` - https://docs.astro.build/en/guides/integrations-guide/tailwind/
- Add DaisyUI: `npm i -D daisyui@latest` - https://daisyui.com/docs/install/
	- Add DaisyUI to Tailwind config
- Add PostCSS: `npm i postcss` - https://www.npmjs.com/package/postcss
	- Add postcss-preset-env: `npm i postcss-preset-env` - https://www.npmjs.com/package/postcss-preset-env
- Add CapacitorJS: - https://capacitorjs.com/docs/getting-started
	- `npm i @capacitor/core`
	- `npm i -D @capacitor/cli`
	- `npm run build` ->  `npx cap init` (www has to be changed to dist) -> `npm i @capacitor/android @capacitor/ios` -> `npx cap add android` -> `npx cap sync` (to open the project with an Android emulator you will need to install Android Studio) - https://developer.android.com/studio
- Add Tauri: `npm install --save-dev @tauri-apps/cli` - https://tauri.app/v1/guides/getting-started/prerequisites (Install these, you will also have to restart your PC)
	- Adjust package.json to include script for tauri - https://tauri.app/v1/guides/getting-started/setup/integrate
	- `npm run tauri init`
	- "../dist"
	- Change port to 4321

That's it! With this we have a Astro project that can use Svelte components. We can easily export to Windows, Linux and Mac with Tauri. We can also easily export to mobile, with CapacitorJS we can use the platforms Android and iOS. And we also have a website.

Useful commands now:
- `npm run dev`: run web server
- `npm run tauri dev`: run tauri & web server
- `npx cap open android`: start android emulator (needs to be synced before)