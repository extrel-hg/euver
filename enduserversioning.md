# End-user versioning 0.3.1 - Summary

Given a version number COMPMAJOR.MINOR.PATCH (e.g., A4.2.1):
* A version with higher precedence must be backward compatible with versions with the same COMP and lower precedence.
* Increment MAJOR when new systems are added.
* Increment MINOR when introducing new features, functionality, content, to already existing systems in your program.
* Increment PATCH when fixing bugs, tweaking features.
* COMP consists of capital letters. MAJOR, MINOR, PATCH consists of non-negative integers, MUST NOT contain leading zeroes, and when incrementing a version, set all following fields to 0.

# Introduction

Semantic Versioning is the de facto standard in software development and management for giving versions to programs with a public API.

However, by definition, you cannot use Semantic Versioning for software without a public API, and while many games do provide an API, information about its version is usually useless to the end-user. So I adapted SemVer for versioning programs for the end-user, not for other developers. I call the new system End-user Versioning, EuVer.

EuVer is meant to inform the end-user about the general compatibility of each version and what changed between versions. The whole system is heavily based on SemVer 2.0.0, but I have added one more field to the classic MAJOR, MINOR and PATCH notation - compatibility (COMP). COMP consists of a series of uppercase letters. The rule is simple: versions with the same COMP must be backward compatible.

I have included an optional set of rules (Rule 11.) for more precisely describing just how much different COMP versions are compatible. 

# Specification

End-user versioning is versioned using Semantic Versioning 2.0.0.

The key words “MUST”, “MUST NOT”, “REQUIRED”, “SHALL”, “SHALL NOT”, “SHOULD”, “SHOULD NOT”, “RECOMMENDED”, “MAY”, and “OPTIONAL” in this document are to be interpreted as described in RFC 2119.

1. Software using End-user versioning MUST be meant for usage by the end-user. If the same software provides a public API, it MUST use Semantic Versioning 2.0.0.
2. A normal version number MUST take the form \<C>X.Y.Z or X.Y.Z, where X, Y, and Z are non-negative integers, and MUST NOT contain leading zeroes. \<C> MUST be a series of uppercase letters. X is the major version, Y is the minor version, and Z is patch version. X,Y and Z MUST increase numerically.
3. Once a versioned package has been released, the contents of that version MUST NOT be modified. Any modifications MUST be released as a new version.
4. Any version number without \<C> is reserved for initial development. Anything MAY change at any time. Data files between versions MAY NOT be interchangeable.
5. When the software exits initial development, \<C> MUST be set to "A", and X.Y.Z to 1.0.0. This is the only time X.Y.Z can be reset.
6. Patch version Z (\<c>x.y.Z) MUST be incremented if only bug fixes or feature tweaks are introduced. A bug fix is defined as an internal change that fixes incorrect behavior. A feature tweak is defined as a small change to only one feature. E.g., changing prices of in-game items.
7. Minor version Y (\<c>x.Y.z) MUST be incremented if new features or content is introduced to the software. It MUST be incremented if any feature or content is removed. It MAY be incremented if multiple feature tweaks are introduced. It MAY include patch level changes. Patch version MUST be reset to 0 when minor version is incremented. A feature is defined as any element of software that is available to users. E.g., Mining out blocks in Minecraft.
8. Major version X (\<c>X.y.z) MUST be incremented if \<C> changes or when new feature systems are added or removed. It MAY also include minor and patch level changes. Patch and minor versions MUST be reset to 0 when major version is incremented. A feature system is defined as multiple features that are interconnected, similar in nature. E.g., The physics of props in Counter-Strike: Source is a feature system, as it connects multiple features of props: ability to be picked up, collision with bullets, rolling, standing still, collision with players etc.
9. COMP (\<C>) (\<C>x.y.z) MUST be the same between all version numbers that are backward compatible with each other. Two versions are backward compatible when the one with higher precedence can successfully read data from the one with lower. If a version is not backward compatible with any other, \<C> MUST change to an unused series of uppercase letters. If a version is compatible with multiple other versions, \<C> MUST be changed to the \<C>, that is lowest in alphabetical order, of a compatible version.
10. A pre-release version MAY be denoted by appending a hyphen and a series of dot-separated identifiers immediately following the patch version. Identifiers MUST comprise only ASCII alphanumerics and hyphens [0-9A-Za-z-]. Identifiers MUST NOT be empty. Identifiers MUST NOT consist of only hyphens. Numeric identifiers MUST NOT include leading zeroes. Pre-release versions have a lower precedence than the associated normal version. A pre-release version indicates that the version is unstable and might not satisfy the intended compatibility requirements as denoted by its associated normal version. Examples: 1.0.0-alpha, 1.0.0-alpha.1, 1.0.0-0.3.7, 1.0.0-x.7.z.92, 1.0.0-x-y-z.
11. Read-write compatibility MAY be denoted by adding an equal sign, followed by a string of uppercase and lowercase characters, digits, and the characters ">", ".", "-", immediately after the patch or pre-release version. The string of characters must follow those rules:
* 1. The string of characters MUST consist of existing \<C> tags or version numbers.
* 2. Each \<C> or version number must be separated by the ">" character.
* 3. All <C> tags MUST be written in lowercase, except for the current version's tag.
* 4. To the left of the current versions tag you MUST put only the \<C> tag of versions, that the current version can successfully read data from, and save it in the current version format. The \<C> refers to the version with highest precedence, that is still lower than the current version. For example, given the versions A1.0.0, A1.1.0, B2.0.0=a>B, A3.0.0, in version B2.0.0=a>B we refer to the latest version of A with a lower precedence than B2.0.0
* 5. To the right of the current versions tag you MUST put only the \<C> tag of versions, that can successfully read and save data written by the current version. We maintain the reference rules outlined in 4.
* 6. You SHOULD NOT omit any \<C> tags that fulfill rules 4. or 5.
* 7. You MUST NOT use a \<C> tag for the current version, if you end up with the another tag on both sides of it. Example: B2.0.0=a>B>a. This means the newest version of A can read B2.0.0, and vice versa. You MUST use A instead.
* 8. You MAY put a \<C> tag of the current version on the right side of the current version. This signals that the current version's files can be read by the earlier version. For example, when given versions A1.0.0, A1.1.0, A1.2.0, A2.0.0=A>a:
* * * All of them are backward compatible with previous ones.
* * * A1.2.0 can read files from A2.0.0.
* 9. You MAY denote an exact version number on either side of the current version. This SHOULD be used sparingly. Example: A1.0.0, A2.0.0, B2.0.0=a1.0.0>B, B2.0.1, B2.1.0=B>b2.0.0
* 10. You MUST NOT update RW compatibility in already released versions. This is prohibited by rule 3. of the specifications. You MAY release a new version with an incremented PATCH number, that contains updated RW compatibility.
* * * Example: A1.0.0, A2.0.0, B3.0.0=a>B. You MAY release version A2.0.1=A>b3.0.0 
* 9. Example: The version BD9.2.1-alpha=b>d>BD>a can successfully read data from versions with COMP B and D, and versions with COMP A can successfully read data from BD. This is assuming versions with COMP A, B and D all are the highest precedence that is still lower than BD9.2.1-alpha=b>d>BD>a.
* 10. RW compatibility system is complex, and you do not need to use it in your versioning. Simply stating what versions the current version can read files from, in for example the README file, may be good enough for you.
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

While SemVer has a very concrete and important problem to solve, EuVer does not. Does this mean EuVer is useless, and everyone should simply use their own versioning system? I disagree.

EuVer provides a versioning system that hopefully could be applied to 99% of games and programs available. The compatibility system should be flexible enough, so that it can be barely used or be very comprehensive about different versions compatibility.

I do not expect my versioning system to be used as universally as SemVer. I do not think my system is better than yours, you may be in a situation where you make a simple game, and all you need is a simple version counter (v1, v2 etc.). I personally tried a few times to find "SemVer for games" online, and found barely anything. So I have written this system so that I can refer to it in my projects, and if somehow anyone finds it and decides this fits their needs, I'll be happy.

I will respond to any questions asked in discussions or issues, and if one question repeats itself multiple times, I'll add it to the FAQ. If you have any ideas on how to edit EuVer to make it more concise, formal, technical (especially the definition of a feature tweak, feature and feature system), please open a pull request and I will look through it.

# FAQ

### How to start a project using EuVer?
Start with version 0.1.0 and increment accordingly to specification. When ready, release A1.0.0. This is the only time you will reset MAJOR.

### How do I know when to release A1.0.0?
When you feel that the data files your program operates on are more-or-less set, you can go A1.0.0. Remember, if a newer version can convert data from an older version, it is the same COMP.

### If even the tiniest change to reading data makes two versions incompatible, won't I end up at HKG4.2.1 very quickly?
When we look at Minecraft we can see that it is possible to make a game that can read game files from 10 years ago. It is your responsibility to make your user be able to access data they created long ago.

### What do I do if I accidentally release a incompatible change to an incorrect COMP?
Fix the problem and release a new version that corrects the change, or makes a new COMP. Even now, do not modify the offending release. Immidietly inform your users about this version. This is a serious risk, and can cause users to lose important data.


# About
Big thanks to [everyone who created](https://github.com/semver/semver/graphs/contributors) and maintained [SemVer 2.0.0](https://semver.org). I modified their versioning system a little, but the bulk of my specification is still their work.

This versioning system is licensed under the [CC 4.0 license](https://creativecommons.org/licenses/by/4.0/).

Originally written by Hubert Gonera.