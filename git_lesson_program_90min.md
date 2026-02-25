# Git Lesson Program (90 minutes, Carpentries-matched)

This version follows the **Software Carpentry Git Novice** content and examples closely (episodes 2 to 9), but trims scope for a 90-minute class.

Primary references:
- Lesson: <https://swcarpentry.github.io/git-novice/index.html>
- Instructor schedule: <https://swcarpentry.github.io/git-novice/instructor/index.html>

Checked on: February 25, 2026.

## Carpentries baseline (episodes 1-9)

From the Carpentries schedule, up to **Conflicts (episode 9)** is:
- 2h35m total = **155 minutes**

Episode starts in Carpentries:
- 1 Automated Version Control: 00:00
- 2 Setting Up Git: 00:05
- 3 Creating a Repository: 00:10
- 4 Tracking Changes: 00:20
- 5 Exploring History: 00:40
- 6 Ignoring Things: 01:05
- 7 Remotes in GitHub: 01:10
- 8 Collaborating: 01:55
- 9 Conflicts: 02:20

## Compression to 90 minutes

- You estimated about 30% faster after live demo.
- 155 x 0.70 = about 109 minutes.
- To fit 90 minutes, we keep Carpentries order/examples but remove optional side content.

## 3 blocks (demo first, then student follow-along)

## Block 1 (0-30 min): Setup + Create + Track

Carpentries alignment: episodes 2, 3, 4

Content and examples:
- `git config --global user.name` / `user.email`
- Create `recipes` repo (`git init`)
- Create and track `guacamole.md`
- `git status`, `git add`, `git commit`, `git diff`, `git log --oneline`

Teaching split:
- 0-10 min: instructor demo
- 10-27 min: students run Block 1 worksheet
- 27-30 min: checkpoint (everyone has 2 commits)

## Block 2 (30-60 min): History + Ignore + Remote basics

Carpentries alignment: episodes 5, 6, 7, 8 (core path)

Content and examples:
- History view: `git diff HEAD~1 guacamole.md`, `git log --oneline`
- Ignore patterns with `.gitignore` using Carpentries-style files (`*.png`, `pictures/`)
- Remote workflow commands in Carpentries order:
  - `git remote add origin ...`
  - `git push origin main`
  - collaborator clone, commit `hummus.md`, `git push`
  - owner `git pull origin main`

Classroom adaptation:
- Use local bare remote instead of GitHub to avoid account/login delays.
- Commands stay the same shape as Carpentries.

Teaching split:
- 30-40 min: instructor demo
- 40-57 min: students run Block 2 worksheet
- 57-60 min: checkpoint (everyone has done one push and one pull)

## Block 3 (60-88 min): Conflicts

Carpentries alignment: episode 9

Content and examples (same pattern as Carpentries):
- Both copies edit the same line in `guacamole.md` instructions
- Non-fast-forward situation
- Pull and inspect conflict markers:
  - `<<<<<<<`
  - `=======`
  - `>>>>>>>`
- Resolve file, then:
  - `git add guacamole.md`
  - `git commit -m "Merge changes from GitHub"`
  - `git push origin main`

Teaching split:
- 60-70 min: instructor demo
- 70-85 min: students run Block 3 worksheet
- 85-88 min: checkpoint (all can explain markers and merge commit)

## Wrap-up (88-90 min)

- Recap loop: `status -> add -> commit -> push/pull -> resolve conflicts`
- Handoff to full Carpentries episodes for self-study details and exercises

## Out-of-class self-study

Continue in the Carpentries lesson, especially deeper parts of:
- Episode 5 (more history navigation)
- Episode 7 (hosted GitHub setup details)
- Episode 8 (collaboration practice)
- Episode 9 (additional conflict scenarios)

Optional hosting target for your cohort:
- VU GitLab sign-in: <https://git.vu.nl/users/sign_in>
