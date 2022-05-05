## Git branches
- Allow you to switch between different versions of your code, which can be developed separately, without conflicting with each other.
- Are implemented as pointers that reference commit hashes. When you’re on a branch, there’s a special pointer called HEAD which references the branch pointer.
- Should be used by developers when implementing changes such as features, fixes and refactors. This keeps the main branch safe from breaking changes.
- With git merge you join one branch into another. This can result in a “merge conflict” if the same lines in a file have been edited on both branches. In these cases you need to resolve the conflict, by indicating to Git what the merged version should look like.

## Gitflow
- Is a branching and release workflow for Git that helps with continuous development.
- Is based on two main branches, master and develop, but work should never be done directly on these branches (on GitHub you can protect them with custom rules).
- Any new feature or fix is developed in a dedicated branch, that can be merged into develop with a pull request once it’s completed.
- Whenever you want to deploy a set of features into production (aka pushing a new release), you merge from develop to master.
- This workflow allows to have the production code in master, the latest features in develop, and any work-in-progress in a dedicated branch.
- The code in master and develop should always be stable, passing the tests, and in a working state.