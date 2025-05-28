# End-user versioning 0.7.0 - Summary

Given a version number COMPMAJOR.MINOR.PATCH (e.g., A4.2.1):
* COMP (uppercase or lowercase letters) denotes compatibility. Versions with the same COMP MUST be backward compatible. Lowercase COMP indicates forward compatibility with the previous version.
* MAJOR changes when new feature systems are added or removed.
* MINOR increments when new features or content are added to existing systems.
* PATCH updates for bug fixes and feature tweaks.

# Introduction

Semantic Versioning is the de facto standard in software development and management for giving versions to programs with a public API.

However, by definition, you cannot use Semantic Versioning for software without a public API, and while many games do provide a public API, information about its version is usually useless to the end-user. So I adapted SemVer for versioning programs for the end-user, not for other developers. I call the new system End-user Versioning, EuVer.

EuVer is meant to inform the end-user about the general compatibility of each version and what changed between versions. The whole system is heavily based on SemVer 2.0.0, but I have added one more field to the classic MAJOR, MINOR and PATCH notation - compatibility (COMP). COMP consists of a series of english alphabet letters. The rule is simple: versions with the same COMP must be backward compatible.

I have included an optional set of rules (Rule 11.) for more precisely describing just how much different COMP versions are compatible. 

# Definitions

1. Forward compatibility is defined, when a version with lower precedence can successfully read data written by a version with higher precedence.
2. Backward compatibility is defined, when a version with higher precedence can read data written by a version with lower precedence.
3. A bug fix is defined as an internal change that fixes incorrect behavior.
4. A feature is defined as a distinct, self-contained functionality or content available to the end user.
5. A feature tweak is defined as a minor modification to a single feature, that does not change its core functionality.
6. A feature system is defined as a collection of interconnected features that function together and rely on each other to form a cohesive unit.
7. Previous version is defined as a version with the highest precedence, that is still lower than the version that is being talked about.
8. Next version is defined as a version with the lowest precedence, that is still higher than the version that is being talked about.
* Example: given the versions A1.0.0, A2.0.0, A3.0.0, the next version of A2.0.0 is A3.0.0, and the previous version of A2.0.0 is A1.0.0.

# Specification

End-user versioning is versioned using Semantic Versioning 2.0.0.

The key words “MUST”, “MUST NOT”, “REQUIRED”, “SHALL”, “SHALL NOT”, “SHOULD”, “SHOULD NOT”, “RECOMMENDED”, “MAY”, and “OPTIONAL” in this document are to be interpreted as described in RFC 2119.

1. Software using End-user versioning MUST be meant for usage by the end-user.
2. A normal version number MUST take the form \<C>X.Y.Z or X.Y.Z, where X, Y, and Z are non-negative integers, and MUST NOT contain leading zeroes. \<C> MUST be a series of english alphabet letters. X is the major version, Y is the minor version, and Z is patch version. X,Y and Z MUST increase numerically, with the exception of moving from initial development to full release.
3. Once a versioned package has been released, the contents of that version MUST NOT be modified. Any modifications MUST be released as a new version.
4. Any version number without \<C> is reserved for initial development. Anything MAY change at any time. Data files between versions MAY NOT be interchangeable.
5. When the software exits initial development, \<C> MUST be set to a valid COMP, and X.Y.Z to 1.0.0. This is the only time X.Y.Z can be reset.
6. Patch version Z (\<c>x.y.Z) MUST be incremented if only bug fixes or feature tweaks are introduced.
7. Minor version Y (\<c>x.Y.z) MUST be incremented if new features or content is introduced to the software. It MUST be incremented if any feature or content is removed. It MAY be incremented if multiple feature tweaks are introduced. It MAY include patch level changes. Patch version MUST be reset to 0 when minor version is incremented.
8. Major version X (\<c>X.y.z) MUST be incremented if \<C> changes or when new feature systems are added or removed. It MAY include minor and patch level changes. Patch and minor versions MUST be reset to 0 when major version is incremented.
9. COMP (\<C>) (\<C>x.y.z) MUST be the same between all version numbers that are backward compatible with each other. If a version is not backward compatible with any other, \<C> MUST change to an unused series of letters. If a version is backward compatible with multiple other versions, \<C> MUST be changed to the \<C>, that is lowest in alphabetical order. If the previous version with the same \<C> is forward compatible with the current one, then write \<C> in lowercase.
10. A pre-release version MAY be denoted by appending a hyphen and a series of dot-separated identifiers immediately following the patch version. Identifiers MUST comprise only ASCII alphanumerics and hyphens [0-9A-Za-z-]. Identifiers MUST NOT be empty. Identifiers MUST NOT consist of only hyphens. Numeric identifiers MUST NOT include leading zeroes. Pre-release versions have a lower precedence than the associated normal version. A pre-release version indicates that the version is unstable and might not satisfy the intended compatibility requirements as denoted by its associated normal version. Examples: 1.0.0-alpha, 1.0.0-alpha.1, 1.0.0-0.3.7, 1.0.0-x.7.z.92, 1.0.0-x-y-z.
11. Read-write compatibility MAY be denoted by adding an equal sign, followed by a string of uppercase and lowercase characters, digits, and the characters ">", ".", "-", immediately after the patch or pre-release version. The string of characters must follow those rules:
* 1. The string of characters MUST consist of existing \<C> tags or version numbers.
* 2. Each \<C> or version number must be separated by the ">" character.
* 3. All <C> tags MUST be written in lowercase, except for the current version's tag.
* 4. To the left of the current versions tag you MUST put only the \<C> tag of versions, that the current version can successfully read data from, and save it in the current version format. The \<C> refers to the latest version with the \<C> tag. For example, given the versions A1.0.0, A1.1.0, B2.0.0=a>B, A3.0.0, in version B2.0.0=a>B we refer to (A3.0.0).
* 5. To the right of the current versions tag you MUST put only the \<C> tag of versions, that can successfully read and save data written by the current version.
* 6. Example of the following rules: version C3.0.0=a>C>b can read data from the latest A version that is older than 3.0.0. The latest B version that is older than 3.0.0 can read data from C3.0.0=a>C>b.
* 7. You SHOULD NOT omit any \<C> tags that fulfill rules 4. or 5.
* 8. You MUST NOT use a \<C> tag for the current version, if you end up with the another tag on both sides of it. Example: B2.0.0=a>B>a. This means the newest version of A can read B2.0.0, and vice versa. You MUST use A for the current \<C> instead.
* 9. You MAY denote an exact version number on either side of the current version. This SHOULD be used sparingly. Example: A1.0.0, A2.0.0, B2.0.0=a1.0.0>B, B2.0.1, B2.1.0=B>b2.0.0
* 10. You MAY denote a range of versions on either side of the current version. This SHOULD be used sparingly. The range must be separated by ">>". Example: B2.1.0=B>a1.0.0>>a2.0.0.
* 11. You MUST NOT update RW compatibility in already released versions. This is prohibited by rule 3. of the specifications. You MAY release a new version with an incremented PATCH number, that contains updated RW compatibility.
* * * Example: A1.0.0, A2.0.0, B3.0.0=a>B. You MAY release version A2.0.1=A>b3.0.0 
* 12. RW compatibility system is complex, and you do not need to use it in your versioning. Simply stating what versions the current version can read files from, in for example the README file, may be good enough for you. I have made this system flexible enough, so that you are not required to use all of its features. Most projects will probably need one or two \<C> tags, and probably won't need to use RW compatibility.
12. Build metadata MAY be denoted by appending a plus sign and a series of dot-separated identifiers immediately following the patch, pre-release version or read-write compatibility. Identifiers MUST comprise only ASCII alphanumerics and hyphens [0-9A-Za-z-]. Identifiers MUST NOT be empty. Identifiers MUST NOT consist of only hyphens. Build metadata MUST be ignored when determining version precedence. Thus two versions that differ only in the build metadata, have the same precedence. Examples: 1.0.0-alpha+001, 1.0.0+20130313144700, 1.0.0-beta+exp.sha.5114f85, 1.0.0+21AF26D3-117B344092BD.
12. Precedence refers to how versions are compared to each other when ordered.
* 1. Precedence MUST be calculated by separating the version into major, minor, patch and pre-release identifiers in that order (Build metadata, comp tag, RW compatibility does not figure into precedence).
* 2. Precedence is determined by the first difference when comparing each of these identifiers from left to right as follows: Major, minor, and patch versions are always compared numerically.
*  * Example: 1.0.0 < 2.0.0 < 2.1.0 < 2.1.1.
* 3. When major, minor, and patch are equal, a pre-release version has lower precedence than a normal version:
* * Example: 1.0.0-alpha < 1.0.0.
* 4. Precedence for two pre-release versions with the same major, minor, and patch version MUST be determined by comparing each dot separated identifier from left to right until a difference is found as follows:
* * 1. Identifiers consisting of only digits are compared numerically.
* * 2. Identifiers with letters or hyphens are compared lexically in ASCII sort order.
* * 3. Numeric identifiers always have lower precedence than non-numeric identifiers.
* * 4. A larger set of pre-release fields has a higher precedence than a smaller set, if all of the preceding identifiers are equal.
* 5. Example: 1.0.0-alpha < 1.0.0-alpha.1 < 1.0.0-alpha.beta < 1.0.0-beta < 1.0.0-beta.2 < 1.0.0-beta.11 < 1.0.0-rc.1 < 1.0.0.

# Why use EuVer?

While SemVer is designed specifically for APIs, EuVer is meant to provide a structured versioning system for end-users, where API stability is not the main concern.

EuVer provides a versioning system that hopefully could be applied to 99% of games and programs available. The compatibility system should be flexible enough, so that it can be barely used or be very comprehensive about different versions compatibility.

I do not expect my versioning system to be used as universally as SemVer. I do not think my system is better than yours. You may be in a situation where you make a simple game, and all you need is a simple version counter (v1, v2 etc.). Despite searching for a standardized versioning system for games, I did not find any established solutions, which motivated me to create EuVer.

I will respond to any questions asked in discussions or issues, and if one question repeats itself multiple times, I'll add it to the FAQ. If you have any ideas on how to edit EuVer to make it more concise, formal, technical (especially the definition of a feature tweak, feature and feature system), please open a pull request and I will look through it.

# FAQ

### How to start a project using EuVer?
Start with version 0.1.0 and increment accordingly to specification. When ready, release A1.0.0. This is the only time you will reset MAJOR.

### How do I know when to release A1.0.0?
When you feel that the data files your program operates on are more-or-less set, you can go A1.0.0. Remember, if a newer version can convert data from an older version, it is the same COMP.

### If even the tiniest change to reading data makes two versions incompatible, won't I end up at HKG4.2.1 very quickly?
When we look at Minecraft we can see that it is possible to make a game that can read game files from 10 years ago. Many software projects (including games like Minecraft) maintain compatibility by using automatic migration scripts, or fallback mechanisms. It is your responsibility to ensure that users can access their old data. Careful planning and testing can help avoid frequent COMP changes.

### What if I mistakenly release an incompatible change without updating COMP?
Fix the problem and release a new version that corrects the change, or makes a new COMP. Even now, do not modify the offending release. Immediately inform your users about this version. This is a serious risk, and can cause users to lose important data.

### What to do if I fix a bug in an old version that causes forward compatibility with the newest version to break?
Example: Given the versions A1.0.0, B2.0.0B>a I release a patch A1.0.1, that somehow breaks compatibility in B2.0.0B>. The reccommended way to fix this is to release B2.0.1.

# About
Big thanks to [everyone who created](https://github.com/semver/semver/graphs/contributors) and maintained [SemVer 2.0.0](https://semver.org). I modified their versioning system a little, but the bulk of my specification is still their work.

This versioning system is licensed under the [CC 4.0 license](https://creativecommons.org/licenses/by/4.0/).

Originally written by Hubert Gonera.