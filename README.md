# BadgeQuest — GitHub Achievement Planner

A responsive, static checklist that helps developers understand GitHub profile achievements and track their personal goals.

**Live demo:** Enable GitHub Pages in the repository settings to publish `index.html` from the `main` branch.

## Features

- Responsive dark UI for desktop and mobile
- Filter achievements by earned, goals, or historical events
- Progress summary updates as the checklist changes
- Checklist state is saved in the current browser using `localStorage`
- Links to GitHub and official profile documentation
- No build step, framework, backend, analytics, or API token required

## Run locally

Open `index.html` in a modern browser. The page is self-contained.

## Enable GitHub Pages

1. Open **Settings → Pages** in this repository.
2. Under the build and deployment settings, select **Deploy from a branch**.
3. Choose branch `main` and folder `/ (root)`, then save.
4. Wait for the deployment to finish; GitHub will show the published URL in Pages settings.

## Important limitations

BadgeQuest is a **manual planner**, not a GitHub account integration. It does not fetch or verify your achievements and cannot grant badges. The checkboxes are personal notes stored only in this browser and do not sync between devices. GitHub controls eligibility, award timing, visibility, and badge tiers; requirements may change. Some achievements depend on other developers' participation, accepted answers, or stars, and historical-event badges cannot be earned today.

Read the [official GitHub profile reference](https://docs.github.com/en/account-and-profile/reference/profile-reference) before relying on eligibility details.

## Contributing

Read [CONTRIBUTING.md](CONTRIBUTING.md) and [TESTING.md](TESTING.md). Suggestions should improve accuracy, accessibility, or developer value rather than encourage artificial activity.

## License

Released under the MIT License. See [LICENSE](LICENSE).
