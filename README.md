# .monk-ci

Org-wide MonkCI configuration for every repository in this organisation.
Push this directory as a repository literally named `.monk-ci`, at the org root:

    git@monkci.github.com:Monk-CI-Test2/.monk-ci.git

Each scan clones it from `<server>/<owner>/.monk-ci` over **https, anonymously**,
so the repository must be public. That is the intended shape: `.monk-ci` holds
policy (disables, severity floors), never proprietary regexes.

The scanned repository's own `.monkci/` is applied on top and wins where the two
clash — including `disable = false`, which re-enables a rule this file turns off.

The layout is the same as any scanned repository's; there is no separate schema.

    .monk-ci/
      .monkci/
        secret-detection-ruleset.toml

This copy is mirrored by `repos/11-org-ruleset.monk-ci/`, the local fixture the
test harness mounts when no org repository is reachable. Change both together or
`11-org-ruleset` will pass locally and fail against the real org.
