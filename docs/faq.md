# Release FAQ

### Which versions are currently supported?

We are supporting the latest version, and the two previous minor series. We also work on the next version being developed, which will become the new stable after its 0.Y.0 release.

You can learn more about the [release support policy](https://github.com/reactwg/react-native-releases/blob/main/docs/support.md#what-versions-are-currently-supported) in the releases repository.

### What is a pick request?

A **pick request** is a request for the React Native Release Crew to include a commit into a specific React Native release.
As the development of React Native happens on `main`, you can request for a specific commit or Pull Request to be included in one of the previous version of React Native.

### How to open a pick request?

Everyone can open a pick request by [filing a GitHub issue via this link](https://github.com/reactwg/react-native-releases/issues/new?assignees=&labels=Type%3A+Pick+Request&projects=&template=pick_request_form.yml&title=%5B0.XX%5D+Title).

### What is a qualified pick request?

Judgement call, but using these dimensions to evaluate:

- Is it a fix for a regression introduced by the current release (for example, did it work in `v0.77.0` but it's broken in `v0.78.0`)?
- Is it a fix for a critical developer workflow?

### What is release blocking?

Judgement call, but using these dimensions to evaluate:

- Is it a new issue on the release candidate?
- Is it breaking a core experience of working in React Native?

### When will my fix make it into a release?

We follow a release cycle that is not strictly monthly - you can read more [about it here](https://github.com/react-native-community/discussions-and-proposals/issues/17). When creating a new release, we cut a new branch from `main` (e.g. `0.77-stable`), with all the merged commits up to this point. After this initial cut, new commits on `main` will only be included on this release if they get manually cherry picked. Otherwise, they will be included in the next stable version (when a new cut from `main` will happen). This means that once a pull request is merged to the [core `react-native` repo](https://github.com/facebook/react-native), it may take one or two months for the changes to make it into a stable React Native release.

### How do I know if my fix/feature is in a certain release?

To determine whether a fix or feature is present in a given release, you will need the commit hash where the fix or feature was added to the `main` branch of the core `react-native` repo. If you know the PR, you can look for the comment from **@facebook-github-bot** that says 'closed this in [COMMIT_HASH]'.

Once you have the commit hash, navigate to `https://github.com/facebook/react-native/commit/<COMMIT_HASH>`. Look closely at the commit message, underneath which you will find a list of tags associated with the commit.
These tags will tell you which releases contains this commit. For example, commit [a6768bfd70187634e587d7b2e92d2b6735a4037e](https://github.com/facebook/react-native/commit/a6768bfd70187634e587d7b2e92d2b6735a4037e) has the following tags as of this writing:

```plain
v0.67.0-rc.3 v0.67.0-rc.2 v0.67.0-rc.1 v0.67.0-rc.0 v0.66.3 v0.66.2 v0.66.1 v0.66.0 v0.66.0-rc.4 v0.66.0-rc.3 v0.66.0-rc.2 v0.66.0-rc.1 v0.66.0-rc.0 latest
```

These tags tell us that the commit first made it into the 0.66 release candidate, eventually landing in the 0.66 stable release. It is also present, as you'd expect, in the 0.67 release candidate (and should make it to 0.67 stable, and so on).

If the commit is only present in `main` (i.e. has no tags), then the commit has yet to be picked up by a release (or it may have been included in a follow up cherry pick for a patch version). You can expect it to be included in the next release candidate that is cut once the designed features have all landed.

### How can I find the status of the current release?

We have a dedicated [release discussions repo](https://github.com/reactwg/react-native-releases/discussions).

Currently we track the progress for the upcoming & supported version of React Native [using GitHub Projects here](https://github.com/reactwg/react-native-releases/projects?query=is%3Aopen).

### What if I find a release blocker that needs escalation?

- Is there an existing release blocking issue?
  - If no, [create a release blocking issue via this form](https://github.com/reactwg/react-native-releases/issues/new/choose).

### What defines which issues and PRs are worked on?

Due to support bandwidth, the React Native team, with the community's help, looks into issues & PRs opened against the supported versions.

Issues & PRs opened against older versions would be considered only in exceptional cases, so we recommend to [update](https://reactnative.dev/docs/upgrading) your applications and libraries to one of the supported versions.

Issues should contain a [**reproducer**](https://stackoverflow.com/help/minimal-reproducible-example) project regardless of which version they target, for them to be considered.
Issues without a reproducer will require more effort to understand and fix, and are less likely to receive attention.

At this point in time, we are prioritizing issues that are related to:

- Latest version of React Native and two previous minor series.
- Use of the New Architecture
- Use of the Hermes Engine

### Security Issues

Meta has [a bounty program](https://www.facebook.com/whitehat/) for the safe disclosure of security bugs. In those cases, please go through the process outlined on that page and do not file a public issue.

## Testing FAQ

### Why is the Hermes version incorrect when testing Android?

Android uses the version of hermes that is built in CI in the maven-local repository. It is expected to see `Engine: Hermes for RN 1000.0.0-zyx`, for example.

<img src="https://cdn.discordapp.com/attachments/1168682018943541429/1295746089625849927/image.png?ex=670fc515&is=670e7395&hm=a062425e4468fc64b77c6e98d6d36c428f549b31f9cb7d87f3e9ff93e3a68c8a&" width="600" />
