# ConVo Neighborhood

The website for ConVo Neighborhood, a branding, consulting and business development firm in Austin, Texas.
Live at [convoneighborhood.com](https://convoneighborhood.com) once the domain is connected.

## How it's built

- [Astro](https://astro.build) static site, hosted on Vercel.
- Brand: the ConVo Neighborhood Branding Blueprint Kit ("Retro Groove"): Espresso, Cream, Gold and Sunset Orange,
  with Shrikhand headlines, Righteous labels and DM Sans body text.

## Where things live

| What | File |
| --- | --- |
| Phone, email, city, menu links | `src/site.js` |
| Services, steps, packages, Neighborhood terms | `src/content.js` |
| Brand colors and fonts | `src/styles/global.css` |
| Pages | `src/pages/` |
| Logo and icons | `public/images/`, `public/favicon.png` |

## Run it

```bash
npm install
npm run dev
```

`npm run build` writes the finished site to `dist/`.
