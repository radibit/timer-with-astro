# ⏲️ Astro Timer

[![Open in StackBlitz](https://developer.stackblitz.com/img/open_in_stackblitz.svg)](https://stackblitz.com/github/radibit/astro-timer/tree/latest)

## 🚀 Project Structure

Inside of the Astro Timer project, you'll see the following folders and files:

```
/
├── public/
│   ├── fonts/
│   ├── robots.txt
│   └── favicon.ico
├── src/
│   ├── components/
│   │   ├── Timer.vue
│   │   └── Tour.astro
│   ├── pages/
│   │   └── index.astro
│   └── styles/
│       └── main.css
└── package.json
```

Astro looks for `.astro` or `.md` files in the `src/pages/` directory.
Each page is exposed as a route based on its file name.

There's nothing special about `src/components/`, but that's where we like to put any Astro/React/Vue/Svelte/Preact components.

Any static assets, like images, can be placed in the `public/` directory.

## 🧞 Commands

All commands are run from the root of the project, from a terminal:

| Command           | Action                                       |
| :---------------- | :------------------------------------------- |
| `npm install`     | Installs dependencies                        |
| `npm run dev`     | Starts local dev server at `localhost:3000`  |
| `npm run build`   | Build your production site to `./dist/`      |
| `npm run preview` | Preview your build locally, before deploying |

## 👀 Want to learn more?

Feel free to check [Astro's documentation](https://github.com/withastro/astro) or jump into their [Discord server](https://astro.build/chat).
