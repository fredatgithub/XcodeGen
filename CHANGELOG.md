# Change Log

## Next Version

## 2.44.1

### Fixed
- Set the correct object version of 77 for Xcode 16 projects @jakobfelsatdm #1563
- Support major.minor SPM package versions which would otherwise fail to decode to a string in yaml specs #1546 @RomanPodymov
- Fix regression for `parallelizable` in scheme. It now resolves to "Enabled" and not "Swift Testing Only" #1565 @CraigSiemens

## 2.44.0

### Added
- Basic support for Xcode 16's synchronized folders #1541 @yonaskolb
  - `TargetSource.type` can now be `syncedFolder`
  - `Options.defaultSourceDirectoryType` can be set to `syncedFolder` for the default type in all sources in the project (defaults to `group`)
  - Benefits include faster generation and no cache invalidation or need to regenerate when files are added or removed from these folders
  - Note that not all TargetSource options like excludes are supported, just a simple path. Please test and see what is missing in your projects
- Added sanitizer options to run and test actions in Scheme #1550 @hi-kumar

### Fixed
- Added validation to ensure that all values in `settings.configs` are mappings. Previously, passing non-mapping values did not raise an error, making it difficult to detect misconfigurations. Now, `SpecParsingError.invalidConfigsMappingFormat` is thrown if misused. #1547 @Ryu0118
- Use `USER` instead of `LOGNAME` for XCUserData #1559 @KostyaSha

## 2.43.0

### Added

- Added `excludeFromProject` from local packages #1512 @maximkrouk
- Added support for `preferredScreenCaptureFormat` in schemes #1450 @vakhidbetrakhmadov

### Changes

- `.appex` files are now copied to plugins directory by default #1531 @iljaiwas
- The `preGenCommand` is now run before validation and caching #1500 #1519 @simonbs @dalemyers
- Improve performance of spec validation #1522 @zewuchen
- The `enableGPUValidationMode` enum is deprecated and is now a boolean #1515 @marcosgriselli @yonaskolb

### Fixed

- **Breaking**: `fileGroups` are now relative paths when in included files, like other paths #1534 @shnhrrsn
- **Breaking**: Local package paths are now relative paths when in included files, like other paths #1498 @juri
- Optional groups are no longer skipped when missing and generating projects from a different directory #1529 @SSheldon

### Internal

- Fix Swift 6.0 warnings #1513 @marcosgriselli
- Update package swift tools to 5.9 #1489 @0111b
- Add Xcode 16 to CI #1439 @giginet
- Fix test project building on CI #1537 @yonaskolb
- Skip failing tests on Linux #1517 @marcosgriselli
- XcodeProj updated to 8.24.3 #1515 @marcosgriselli @yonaskolb

## 2.42.0

### Added

- Better support for local Swift packages in Xcode 15 #1465 @kinnarr
- Added `macroExpansion` to test actions in schemes #1468 @erneestoc

### Changed

- Better default macroExpansion target in schemes #1471 @erneestoc

### Removed

- Removed `xcodegen dump --type graphviz` as graphviz no longer builds in Swift 6 and is no longer maintained. If anyone uses this feature and wishes to keep it, please submit a PR providing a suitable alternative. #1485 @giginet

## 2.41.0

### Added

- Added `xcodegen cache` command that writes the cache. Useful for `post-commit` git hook integration #1476 @yonaskolb

### Changed

- Include folders in file sorting #1466 @jflan-dd

### Fixed

- Fixed `supportedDestinations` validation when it contains watchOS for multiplatform apps. #1470 @tatsuky

## 2.40.1

### Fixed

- Reverted `.xcprivacy` handling. They will now again be treated as resources by default @yonaskolb

## 2.40.0

### Added

- Added support for local Swift packages at the project root by specifying a "" group #1413 @hiltonc
- Added a custom `shell` to a scheme's pre and post actions #1430 @balazs-vimn

### Changed

- `.xcprivacy` files are now not added to any build phases by default #1464 @yonaskolb

## 2.39.1

### Added

- Proper defaults for `.cp` and `.cxx` files #1447 @eschwieb

### Fixed

- Fixed bundle access crash #1448 @freddi-kit
- Pinned XcodeProj version to fix breaking changes when XcodeGen is used as a dependency #1449 @yonaskolb

## 2.39.0

### Added

- Support Artifact Bundle #1388 @freddi-kit
- Added support for `.xcstrings` String Catalogs #1421 @nicolasbosi95
- Added default `LD_RUNPATH_SEARCH_PATHS` for visionOS #1444 @Dahlgren
- Added `watchOS` as a supported cross platform destination #1438 @tatsuky

### Fixed

- Fixed custom local package groups not being created #1416 @JaapManenschijn
- Fixed spec validation error type #1439 @Lutzifer
- Create parent group for local package groups if it does not exist already #1417 @JaapManenschijn

### Internal

- Updated Rainbow version #1424 @nysander

## 2.38.0

### Added

- [Multi-destination targets](https://github.com/yonaskolb/XcodeGen/blob/master/Docs/ProjectSpec.md#supported-destinations) #1336 @amatig
  - Added `supportedDestinations` to target
  - Added optional new `platform` value of `auto` when using `supportedDestinations`
  - Added `destinationFilters` for sources and dependencies
  - Added `inferDestinationFiltersByPath`, a convenience filter for sources
- `.mlpackage` files now default to being a source type #1398 @aaron-foreflight
- Added support for `Build Tool Plug-ins` in `AggregateTarget` #1390 @BarredEwe

### Fixed

- Fixed source file `includes` not working when no paths were found #1337 @shnhrrsn
- Supports specifying multiple package products #1395 @simonbs

## 2.37.0

### Added

- Added support for adding `Build Tool Plug-ins` to targets #1374 @BarredEwe

## 2.36.1

### Fixed

- Revert addition of `ENABLE_MODULE_VERIFIER` build setting for causing issues in tests and some setups #1387 @yonaskolb

## 2.36.0

### Added

- Added `scheme.enableGPUValidationMode` #1294 @LouisLWang
- Added visionOS support #1379 @shiba1014
- Added ability to disable Thread performance checker in Schemes #1380 @piellarda
- Added support for `RuntimeIssue` breakpoints #1384 @yonaskolb

### Changed

- The project object version has been updated for Xcode 14.3 #1368 @leonardorock
- Updated recommended settings for Xcode 14.3 #1385 @yonaskolb
- Dropped support for Xcode 12 and 13, due to XcodeProj update #1384 @yonaskolb

### Fixed

- Fix external dependencies from being removed by Xcode #1354 @OdNairy
- Stop creating orphaned object references when reusing references to external dependencies #1377 @liamnichols

## 2.35.0

### Added

- Added support for shared breakpoints #177 @alexruperez @myihsan
- Added support for `putResourcesBeforeSourcesBuildPhase` in a target #1351 @mat1th

### Fixed

- Fix case where source paths may not be deduplicated correctly resulting in duplicate groups and/or a crash in running Xcodegen #1341 @dalemyers

## 2.34.0

### Changed

- Added support for `swiftcrossimport` folders. #1317 @Iron-Ham
- Added support for [Scheme Management](Docs/ProjectSpec.md##scheme-management) #1142 @wendyliga, @teameh

### Fixed

- Fix includes when the projectRoot is a relative path #1262 @CraigSiemens
- Renamed build phase `Embed App Extensions` to `Embed Foundation Extensions` to fix Xcode 14 warning #1310 @casperriboe

## 2.33.0

### Added

- Added support for `enableGPUFrameCaptureMode` #1251 @bsudekum
- Config setting presets can now also be loaded from the main bundle when bundling XcodeGenKit #1135 @SofteqDG
- Added ability to generate multiple projects in one XcodeGen launch #1270 @skofgar
- Use memoization during recursive SpecFiles creation. This provides a drastic performance boost with lots of recursive includes #1275 @ma-oli

### Fixed

- Fix scheme not being generated for aggregate targets #1250 @CraigSiemens
- Fix recursive include path when relativePath is not set #1275 @ma-oli
- Include projectRoot in include paths #1275 @ma-oli

### Internal
- Updated to Yams 5.0.1 #1297 @s2mr
- Delete ignored `try` keyword #1298 @s2mr

## 2.32.0

### Added

- Add support for `mlmodelc` files #1236 @antonsergeev88
- Add `enable` option for `include` #1242 @freddi-kit

### Fixed

- Fix checking environment variable in `include` #1242 @freddi-kit
- Fix profile action for frameworks in Xcode 14 #1245 @SSheldon

## 2.31.0

### Added

- Added a new CopyFilesBuildPhase, "Embed ExtensionKit Extensions" #1230 @mtj0928
- Added duplicate dependencies validation #1234 @aleksproger

## 2.30.0

### Added

- Added support for new target type `extensionkit-extension` in Xcode 14 #1228 @aleksproger

### Changed

- Speed up generating build settings for large projects #1221 @jpsim

### Fixed

- Fix XcodeGen building as library after breaking XcodeProj update 8.8.0 #1228 @aleksproger

## 2.29.0

Some support for Xcode Test Plans has been added. For now test plans are not generated by XcodeGen and must be created in Xcode and checked in, and then referenced by path. If the test targets are added, removed or renamed, the test plans may need to be updated in Xcode

#### Added

- Schemes and Target Schemes can now reference existing Test Plans under `{scheme}.test.testPlans` and `{target}.scheme.testPlans`, respectively. #716 @yonaskolb @omares

#### Fixed

- Fixed an issue where DocC was not added to source file list #1202 @hiragram

#### Changed

- Updated XcodeProj to 8.7.1 #1213 @yonaskolb

## 2.28.0

#### Added

- Support for specifying custom group locations for SPM packages. #1173 @John-Connolly

### Fixed

- Fix Monterey macOS shell version, shell login flag for environments #1167 @bimawa
- Fixed crash caused by a simultaneous write during a glob processing #1177 @tr1ckyf0x

### Changed

- Run target source pattern matching in parallel #1197 @alvarhansen

## 2.27.0

#### Added

- Support test target for local Swift Package #1074 @freddi-kit
- Added `coverageTargets` for target test schemes. This enables to gather code coverage for specific targets. #1189 @gabriellanata
- Fixed issue where .gyb files could not be added to source file list #1191 @hakkurishian

### Fixed

- Fixed crash caused by a simultaneous write during a glob processing #1177 @tr1ckyf0x
- Skip generating empty compile sources build phases for watch apps #1185 @evandcoleman

## 2.26.0

### Added

- Added the option to specify a `location` in a test target #1150 @KrisRJack

### Changed

- Speed up source inclusion checking for big projects #1122 @PaulTaykalo

## 2.25.0

### Added

- Allow specifying a `copy` setting for each dependency. #1038 @JakubBednar

### Fixed

- Fix broken codesign option for bundle dependency #1104 @kateinoigakukun
- Ensure fileTypes are mapped to JSON value #1112 @namolnad
- Fix platform filter for package dependecies #1123 @raptorxcz
- Fix Xcode 13 build #1130 @raptorxcz @mthole

### Changed

- Update XcodeProj to 8.2.0 #1125 @nnsnodnb

## 2.24.0

### Added

- Added support for DocC Catalogs #1091 @brevansio
- Added support for "driver-extension" and "system-extension" product types #1092 @vgorloff
- Add support for conditionally linking dependencies for specific platforms #1087 @daltonclaybrook
- Add ability to specify UI testing screenshot behavior in test schemes #942 @daltonclaybrook

### Changed

- **Breaking**: Rename the `platform` field on `Dependency` to `platformFilter` #1087 @daltonclaybrook

## 2.23.1

### Changed

- Reverted "Change FRAMEWORK_SEARCH_PATH for xcframeworks (#1015)", introduced in 2.20.0. XCFrameworks need to be
  referenced directly in the project for Xcode's build system to extract the appropriate frameworks #1081 @elliottwilliams

## 2.23.0

#### Added

- Added ability to set custom platform for dependency #934 @raptorxcz

#### Fixed

- Added `()` to config variant trimming charater set to fix scheme config variant lookups for some configs like `Debug (Development)` that broke in 2.22.0 #1078 @DavidWoohyunLee
- Fixed Linux builds on Swift 5.4 #1083 @yonaskolb

## 2.22.0

#### Added

- Support `runPostActionsOnFailure` for running build post scripts on failing build #1075 @freddi-kit

#### Changed

- Xcode no longer alerts to project changes after regeneration, due to internal workspace not regenerating if identical #1072 @yonaskolb

#### Fixed

- Fixed no such module `DOT` error when package is used as a dependency #1067 @yanamura
- Fixed scheme config variant lookups for some configs like `ProdDebug` and `Prod-Debug` that broke in 2.21.0 #1070 @yonaskolb

## 2.21.0

#### Added

- Support weak link for Swift Package Dependency #1064 @freddi-kit

#### Changed

- Carthage frameworks are no longer embedded for "order-only" target dependencies. This avoid redundant embeds in situations where a target's sources _import_ a Carthage framework but do not have a binary dependency on it (like a test target which runs in a host app). #1041 @elliottwilliams

#### Fixed

- The `Core` target is renamed to avoid collisions with other packages. #1057 @elliottwilliams
- Lookup scheme config variants by whole words, fixing incorrect assignment in names that contain subtrings of each other (eg PreProd and Prod) #976 @stefanomondino

## 2.20.0

#### Added

- Allow specifying a `github` name like `JohnSundell/Ink` instead of a full `url` for Swift Packages #1029 @yonaskolb
- Added explicit `LastUpgradeCheck` and `LastUpgradeVersion` override support so it's possible to override these properties without using the `project.xcodeVersion`. [1013](https://github.com/yonaskolb/XcodeGen/pull/1013) @Andre113
- Added `macroExpansion` for `run` in `schemes` #1036 @freddi-kit
- Added `askForAppToLaunch` for `profile` in `schemes` #1035 @freddi-kit
- Added support for selectedTests in schemes `Test` configuration. #913 @ooodin

#### Fixed

- Fixed regression on `.storekit` configuration files' default build phase. #1026 @jcolicchio
- Fixed framework search paths when using `.xcframework`s. #1015 @FranzBusch
- Fixed bug where schemes without a build target would crash instead of displaying an error #1040 @dalemyers
- Fixed files with names ending in **Info.plist** (such as **GoogleServices-Info.plist**) from being omitted from the Copy Resources build phase. Now, only the resolved info plist file for each specific target is omitted. #1027 @liamnichols

#### Internal

- Build universal binaries for release. XcodeGen now runs natively on Apple Silicon. #1024 @thii

## 2.19.0

#### Added

- Added support for building and running on Linux platforms. Tested for compatibility with Swift 5.3+ and Ubuntu 18.04. #988 @elliottwilliams
- Added `useBaseInternationalization` to Project Spec Options to opt out of Base Internationalization. #961 @liamnichols
- Added `storeKitConfiguration` to allow specifying StoreKit Configuration in Scheme and TargetScheme, supporting either xcodeproj or xcworkspace via `schemePathPrefix` option. #964 @jcolicchio
- Added more detailed error message with method arguments. #990 @bannzai
- Added `basedOnDependencyAnalysis` to Project Spec Build Script to be able to choose not to skip the script. #992 @myihsan
- Added `BuildRule.runOncePerArchitecture` to allow running build rules once per architecture. #950 @sascha
- Added discovered dependency file for a build script #1012 @polac24 @fggeraissate

#### Changed

- **Breaking**: Info.plists with custom prefixes are no longer added to the Copy Bundle Resources build phase #945 @anivaros
- **Breaking**: `workingDirectory` of included legacy targets is now made relative to including project #981 @jcolicchio
- **Breaking**: Make `simulateLocation` respect `schemePathPrefix` option. #973 @jcolicchio

#### Fixed

- Fixed error message output for `minimumXcodeGenVersion`. #967 @joshwalker
- Remove force-unwrapping causing crash for `LegacyTarget`s #982 @jcolicchio
- Fixed a race condition in an internal JSON decoder, which would occasionally fail with an error like `Parsing project spec failed: Error Domain=Unspecified error Code=0`. #995 @elliottwilliams
- Fixed issue where frameworks with `MACH_O_TYPE: staticlib` were being incorrectly embedded. #1003 @mrabiciu

#### Internal

- Updated to Yams 4.0.0 #984 @swiftty

## 2.18.0

#### Added

- Add `Scheme.Test.TestTarget.skipped` to allow skipping of an entire test target. #916 @codeman9
- Added ability to set custom LLDBInit scripts for launch and test schemes #929 @polac24
- Adds App Clip support. #909 @brentleyjones @dflems
- Application extension schemes now default to `launchAutomaticallySubstyle = 2` and the correct debugger and launcher identifiers #932 @brentleyjones
- Updated SettingsPresets to use new defaults from Xcode 12. #953 @liamnichols
- Enable Base Internationalization by default as per Xcode 12 behavior. #954 @liamnichols

#### Changed

- Change default project version to Xcode 12 #960 @yonaskolb

#### Internal

- Updates CI to run on Xcode 12. #936 @dflems @yonaskolb

#### Fixed

- Select the first runnable build target, if present. #957 @codeman9
- Allow SDK dependencies to be embedded. #922 @k-thorat
- Allow creating intermediary groups outside of the project directory. #892 @segiddins
- Fix appex's Runpath Search Paths under macOS target. #952 @rinsuki
- `onlyCopyFilesOnInstall` is extended for the Embed App Extensions build phase. #948 @RomanPodymov

## 2.17.0

#### Added

- Added `options.fileTypes` which lets you set cross project defaults for certain file extensions #914 @yonaskolb
- Added `onlyCopyFilesOnInstall` option to targets for the Embed Files build phase. #912 @jsorge

#### Fixed

- Treat all directories with known UTI as file wrapper. #896 @KhaosT
- Generated schemes for application extensions now contain `wasCreatedForAppExtension = YES`. #898 @muizidn
- Allow package dependencies to use `link: false` #920 @k-thorat
- Fixed issue computing relative paths.  #915 @andrewreach

#### Internal

- Updated to XcodeProj 7.13.0 #908 @brentleyjones

## 2.16.0

#### Added

- Improve speed of metadata parsing and dependency resolution. #803 @michaeleisel
- Improve support for iOS sticker packs and add support for `launchAutomaticallySubstyle` to run schemes. #824 @scelis
- Add --project-root option to generate command. #828 @ileitch
- Add an ability to set an order of groups with `options.groupOrdering` #613 @Beniamiiin
- Add the ability to output a dependency graph in graphviz format #852 @jeffctown
- Adds uncluttering the project manifest dumped to YAML from empty values #858 @paciej00
- Added ability to name the executable target when declaring schemes. #869 @elland
- Added ability to set executable to Ask to Launch. #871 @pinda

#### Fixed

- Fixed issue when linking and embedding static frameworks: they should be linked and NOT embed. #820 @acecilia
- Fixed issue when generating projects for paths with a dot in the folder for swift sources. #826 @asifmohd
- Prefix static library target filenames with 'lib' to match Xcode. #831 @ileitch
- Fixed duplicate addition of carthage static frameworks. #829 @funzin
- Fix handling of SWIFT_INSTALL_OBJC_HEADER when its value is YES/NO. #827 @ileitch
- Set `preActions` and `postActions` on the `build` action of a TargetScheme instead of the other actions. #823 @brentleyjones
- Prevent test targets from being set as a scheme's launch action #835 @brentleyjones
- Implicitly include bundles in the Copy Bundle Resources build phase. #838 @skirchmeier
- Fixed dumping a project manifest which contains an array of project references #840 @paciej00
- Generate correct PBXTargetDependency for external targets. #843 @ileitch
- Fix linking of multiple products from the same Swift Package #830 @toshi0383
- Don't deduplicate files in `include` with different path but same name. #849 @akkyie
- Don't link transitive static carthage libraries. #853 @akkyie
- Optimize simplifying paths for faster project generation. #857 @akkyie
- Fixed issue where wrapper folders may not include correctly in the generated project. #862 @KhaosT
- Compile `xcmappingmodel` files instead of copying bundle resources. #834 @jcolicchio
- Fixed issue where `Complie Sources` build phase is generated for resource bundles even when they have no files to compile #878 @nkukushkin

## 2.15.1

#### Fixed

- Fixed issue which caused watch app schemes to be generated incorrectly, preventing these apps from launching. #798 @daltonclaybrook
- Added build presets for the target type `framework.static`. #819 @acecilia
- Fixed XcodeProj resolution and updated to 7.10.0 #822 @soffes

## 2.15.0

#### Added

- Add support for local Swift Packages in `packages` using `path`. #808 @freddi-kit
- Add `buildImplicitDependencies` as an option on `TargetScheme`. #810 @evandcoleman

#### Fixed

- Fixed resolving path to local Swift Packages #796 @freddi-kit
- Added ability to stop on every main thread checker issue on Run schemes and TargetSchemes #799 @ionutivan
- Avoid copying ObjC interface header when SWIFT_INSTALL_OBJC_HEADER=false. #805 @kateinoigakukun

## 2.14.0

#### Added

- Add ability to embed and code sign Swift package dependencies with dynamic products. #788 @alexruperez

#### Fixed

- Revert "Add Base to known regions even if one doesn't exist" #791 @bryansum
- Set `defaultConfigurationName` for every target which is defined in a project. #787 @ken0nek
- Set `TEST_TARGET_NAME` only when a project has UITest bundle. #792 @ken0nek
- Set xcodeproj path in project.xcworkspace/contents.xcworkspacedata #793 @ken0nek

## 2.13.1

#### Fixed

- Validate scheme test action and test coverage target references before generating. #775 @liamnichols
- Fixed parsing prerelease identifiers in Swift package versions #779 @yonaskolb
- Fixed using legacy targets as dependencies #778 @yonaskolb

#### Internal

- Updated to XcodeProj 7.8.0 #777 @yonaskolb
- Use <https://github.com/mxcl/Version> #779 @yonaskolb

## 2.13.0

#### Added

- Support External Target References via subprojects. #701 @evandcoleman

#### Fixed

- Fixed compilation as library by locking down XcodeProj version #767 @yonaskolb
- Stabilized sorting of groups with duplicate names/paths. #671 @ChristopherRogers
- Moved `Copy Bundle Resources` to after `Link with Libraries` build phase #768 @yonaskolb

#### Internal

- Updated to XcodeProj 7.7.0 #767 @yonaskolb

## 2.12.0

#### Added

- Added pre and post command options. Useful for running `pod install` in combination with `--use-cache` #759 @yonaskolb
- Support for language and region settings on a target basis #728 @FranzBusch
- Added option to generate only Info.plist files with `--only-plists` #739 @namolnad
- Added the option to specify a `simulateLocation` in a scheme #722 @basvankuijck
- Support for On Demand Resources tags #753 @sipao

#### Fixed

- Fixed resolving a relative path for `projectReference.path` #740 @kateinoigakukun
- Don't add framework dependency's directory to `FRAMEWORK_SEARCH_PATHS` if it is implicit #744 @ikesyo @yutailang0119
- Fixed resolving relative path passed to `XcodeProj` #751 @PycKamil
- Prefer configurations named "Debug" or "Release" for default scheme build configurations #752 @john-flanagan
- Added an extra check for package versions. #755 @basvankuijck

#### Internal

- Update to SwiftCLI 6.0 and use the new property wrappers #749 @yonaskolb

## 2.11.0

#### Added

- Add Carthage static framework dependencies support. #688 @giginet
- Added `xcodegen dump` command #710 @yonaskolb
- Added `--no-env` option to disable environment variables expansion #704 @rcari
- Added custom group support for target sources #621 @sroebert @rcari
- Added new dependency type, `bundle`. This allows targets to copy bundles from other projects #616 @bsmith11

#### Fixed

- Improved variable expansion runtime #704 @rcari
- Fixed missing headers for static framework targets #705 @wag-miles
- Using more file types from XcodeProj for PBXFileReferences resulting in less project diffs #715 @yonaskolb
- Fixed localized `*.intentdefinition` not being added to build source phases #720 @giginet
- Fixed `selectedLauncherIdentifier` not being set `Xcode.IDEFoundation.Launcher.PosixSpawn` when `debugEnabled: false` is defined in test action #725 @ken0nek
- Fixed unnecessary dependencies related to SwiftPM #726 @tid-kijyun

#### Changed

- Deprecated `$old_form` variables in favor of `${new_form}` variables #704 @rcari
- Updated XcodeProj to 7.4.0 #709 @yonaskolb
- Updated to Swift 5.1 #714 @yonaskolb

## 2.10.1

#### Fixed

- Add Base to knownRegions even if one doesn't exist #694 @bryansum
- Fixed missing `onlyGenerateCoverageForSpecifiedTargets` issue #700 @kateinoigakukun
- Fixed regression on dependencies `link` flag #703 @rcari

## 2.10.0

#### Added

- Support Target Reference to another project. #655 @kateinoigakukun
- Added `coverageTargets` for test target. This enables to gather code coverage for specific targets. #656 @kateinoigakukun

#### Fixed

- Add base localisation by default even if no base localised files were found. Fixes warning in Xcode 11 #685 @yonaskolb
- Don't generate CFBundleExecutable in default generated Info.plist for `bundle` target types #689 @FranzBusch
- Fixed resolving relative paths with custom project destination #681 @giginet
- Fixed resolving relative paths for Info.plist #683 @giginet
- Fixed macOS unit test target TEST_HOST #696 @mjarvis

#### Internal

- Restructure targets #698 @yonaskolb

## 2.9.0

#### Added

- Added Scheme Templates #672 @bclymer

#### Fixed

- Fixed macOS unit test setting preset #665 @yonaskolb
- Add `rcproject` files to sources build phase instead of resources #669 @Qusic
- Prefer default configuration names for generated schemes #673 @giginet
- Fixed some resource files being placed to "Recovered References" group #679 @nivanchikov

#### Internal

- Updated to SwiftCLI 5.3.2 #667 @giginet
- Fixed tests in case-sensitive file system #670 @Qusic

## 2.8.0

#### Added

- Added support for Swift Package dependencies #624 @yonaskolb
- Added `includes` to `sources` for a Target. This follows the same glob-style as `excludes` but functions as a way to only include files that match a specified pattern. Useful if you only want a certain file type, for example specifying `**/*.swift`. #637 @bclymer
- Support `dylib` SDK. #650 @kateinoigakukun
- Added `language` and `region` options for `run` and `test` scheme #654 @kateinoigakukun
- Added `debugEnabled` option for `run` and `test` scheme #657 @kateinoigakukun

#### Fixed

- Expand template variable in Array of Any #651 @kateinoigakukun
- Significantly improve performance when running with a large number files. #658 @kateinoigakukun
- Removed some more diffs between the generated .pbxproj and when Xcode resaves it #663 @yonaskolb

#### Internal

- Removed needless `Array` initialization. #661 @RomanPodymov
- Updated to XcodeProj 7.1.0 #624 @yonaskolb

## 2.7.0

#### Added

- Added Bash 4 style recursive globbing (`**/*`) in target sources `excludes` #636 @bclymer
- Added ability to disable main thread checker in Schemes #601 @wag-miles

#### Fixed

- Fixed included specs that were referenced multiple times from duplicating content #599 @haritowa
- Fixed `.orig` files being added to the project #627 @keith

#### Changed

- Allow linking of dependencies into static libraries when `link` is set to true #635 @kateinoigakukun

## 2.6.0

#### Added

- Added ability to skip tests #582 @kadarandras
- Added ability to set `attributes` on build files #583 @min
- Allow using environment variables in the form of `${SOME_VARIABLE}`. This might be a **breaking** change when a target template attribute is also defined as an environment variable #594 @tomquist
- Added support for `watchapp2-container` and `framework.static` product types #604 @yonaskolb

#### Fixed

- Fixed `.pch` files being bundled as resources #597 @thii
- Fixed an issue that prevents watchOS Intents Extension from running correctly. #571 @KhaosT

#### Changed

- Updated the default `compatibilityVersion` project setting from `Xcode 9.3` to `Xcode 10.0` #581 @acecilia
- Updated to XcodeProj 7.0.0. Note that the length of generated UUIDs has changed #604 @yonaskolb

#### Internal

- Added ability to encode ProjectSpec #545 @ryohey

## 2.5.0

#### Added

- Added support for `app-extension.intents-service` target type #536 @yonaskolb
- Added support for custom `root` in `sdk` dependency #562 @raptorxcz

#### Changed

- Updated to xcodeproj 6.7.0 including its performance improvements #536 @yonaskolb
- Updated default generated settings for Xcode 10.2 #555 @yonaskolb
- Changed order of file generation so that plists are now generated before the project, so they will be included in the projects files #544 @tomquist
- Updated Yams to 2.0.0 @yonaskolb

#### Fixed

- Fixed groups from sources outside a project spec's directory from being flattened. #550 @sroebert
- Fixed `optional` file sources not being added to the project #557 @yonaskolb
- Fixed Carthage dependencies being incorrectly embedded in WatchKit app bundles instead of a WatchKit app extension #558 @KhaosT

## 2.4.0

#### Fixed

- Fixed installation when building in Swift 5 #549 @yonaskolb

#### Changed

- Updated to Swift 5 and dropped Swift 4.2 #549 @yonaskolb

## 2.3.0

#### Added

- Added ability to automatically find all the frameworks for Carthage dependencies via the global `options.findCarthageFrameworks` or dependency specific `dependency.findFrameworks`. See the [Carthage](Docs/Usage.md#carthage) usage docs for more info #506 @rpassis @yonaskolb
- Added support for nested target templates #534 @tomquist
- Added ability to define `templateAttributes` within a target to be able to parameterize templates. #533 @tomquist
- Added ability to set `link` to false in framework dependencies #532 @dimatosaurus
- Added `missingConfigFiles` to `options.disabledValidations` to optionally skip checking for the existence of config files.
- Added ability to define a per-platform `deploymentTarget` for Multi-Platform targets. #510 @ainopara

#### Changed

- **DEPRECATION**: Placeholders `$target_name` and `$platform` have been deprecated in favour of `${target_name}` and `${platform}`. Support for the old placeholders will be removed in a future version #533 @tomquist

#### Fixed

- Sources outside a project spec's directory will be correctly referenced as relative paths in the project file. #524
- Fixed error when `optional` directory source is missing #527 @yonaskolb
- Fixed excludes within included spec #535 @yonaskolb
- Fixed paths in target templates within included files not being relative #537 @yonaskolb
- Fix multi-platform target templates #541 @yonaskolb
- Fixed sources in an included target not being relative when the sources are mix of string and dictionaries #542 @yonaskolb

## 2.2.0

#### Added

- Added ability to generate empty directories via `options.generateEmptyDirectories` #480 @Beniamiiin
- Added support for the `instrumentsPackage` product type #482 @ksulliva
- Added support for `inputFileLists` and `outputFileLists` within project build scripts #500 @lukewakeford
- Added support for a `$target_name` replacement string within target templates #504 @yonaskolb
- Added `createIntermediateGroups` to individual Target Sources which overrides the top level option #505 @yonaskolb

#### Changed

- **BREAKING**: All the paths within `include` files are now relative to that file and not the root spec. This can be disabled with a `relativePaths: false` on the include. See the [documentation](https://github.com/yonaskolb/XcodeGen/blob/master/Docs/ProjectSpec.md#include) for more details #489 @ellneal
- Updated the Xcode compatibility version from 3.2 to 9.3 #497 @yonaskolb
- Exact matches to config names in build settings won't partial apply to other configs #503 @yonaskolb
- UUIDs in the project are standard and don't contain any type prefixes anymore

#### Fixed

- Fixed `--project` argument not taking effect #487 @monowerker
- Fixed Sticker Packs from generating an empty Source file phase which caused in error in the new build system #492 @rpassis
- Fixed generated schemes for tool targets not setting the executable #496 @yonaskolb
- Fixed resolving Carthage dependencies for iOS app with watchOS target. [465](https://github.com/yonaskolb/XcodeGen/pull/465) @raptorxcz

## 2.1.0

#### Added

- Added an experiment new caching feature. Pass `--use-cache` to opt in. This will read and write from a cache file to prevent unnecessarily generating the project. Give it a try as it may become the default in a future release #412 @yonaskolb

#### Changed

- Changed spelling of build phases to **preBuildPhase** and **postBuildPhase**. The older names are deprecated but still work [402](https://github.com/yonaskolb/XcodeGen/pull/402) @brentleyjones
- Moved generation to a specific subcommand `xcodegen generate`. Simple `xcodegen` will continue to work for now #437 @yonaskolb
- If `INFOPLIST_FILE` has been set on a target, then an `info` path won't ovewrite it #443 @feischl97

#### Fixed

- Fixed XPC Service package type in generated `Info.plist` #435 @alvarhansen
- Fixed phase ordering for modulemap and static library header Copy File phases. [402](https://github.com/yonaskolb/XcodeGen/pull/402) @brentleyjones
- Fixed intermittent errors when running multiple `xcodegen`s concurrently #450 @bryansum
- Fixed `--project` argument not working #437 @yonaskolb
- Fixed unit tests not hooking up to host applications properly by default. They now generate a `TEST_HOST` and a `TestTargetID` #452 @yonaskolb
- Fixed static libraries not including external frameworks in their search paths #454 @brentleyjones
- Add `.intentdefinition` files to sources build phase instead of resources #442 @yonaskolb
- Add `mlmodel` files to sources build phase instead of resources #457 @dwb357

## 2.0.0

#### Added

- Added `weak` linking setting for dependencies #411 @alvarhansen
- Added `info` to targets for generating an `Info.plist` #415 @yonaskolb
- Added `entitlements` to targets for generating an `.entitlement` file #415 @yonaskolb
- Added `sdk` dependency type for linking system frameworks and libs #430 @yonaskolb
- Added `parallelizable` and `randomExecutionOrder` to `Scheme` test targets in an expanded form #434 @yonaskolb
- Validate incorrect config setting definitions #431 @yonaskolb
- Automatically set project `SDKROOT` if there is only a single platform within the project #433 @yonaskolb

#### Changed

- Performance improvements for large projects #388 @yonaskolb @kastiglione
- Upgraded to xcodeproj 6 #388 @yonaskolb
- Upgraded to Swift 4.2 #388 @yonaskolb
- Remove iOS codesigning sdk restriction in setting preset #414 @yonaskolb
- Changed default project version to Xcode 10.0 and default Swift version to 4.2 #423 @yonaskolb
- Added ability to not link Carthage frameworks #432 @yonaskolb

#### Fixed

- Fixed code signing issues #414 @yonaskolb
- Fixed `TargetSource.headerVisibility` not being set in initializer #419 @jerrymarino
- Fixed crash when using Xcode Legacy targets as dependencies #427 @dflems

## 1.11.2

If XcodeGen is compiled with Swift 4.2, then UUID's in the generated project will not be deterministic. This will be fixed in an upcoming release with an update to xcodeproj 6.0

#### Fixed

- Fixed release builds in Swift 4.2 #404 @pepibumur
- Fixed default settings for macOS unit-tests #387 @frankdilo
- Fixed Copy Headers phase ordering for Xcode 10 #401 @brentleyjones
- Fixed generated schemes on aggregate targets #394 @vgorloff

#### Changed

- Added `en` as default value for knownRegions #390 @Saik0s
- Update `PathKit`, `Spectre`, `Yams` and `xcodeproj` dependencies

## 1.11.1

#### Fixed

- Fixed `FRAMEWORK_SEARCH_PATHS` for `framework` dependency paths with spaces #382 @brentleyjones
- Fixed aggregate targets not being found with `transitivelyLinkDependencies` #383 @brentleyjones

## 1.11.0

#### Added

- Added `showEnvVars` to build scripts to disable printing the environment #351 @keith
- Added `requiresObjCLinking` to `target` #354 @brentleyjones
- Added `targetTemplates` #355 @yonaskolb
- Added `aggregateTargets` #353 @yonaskolb
- Added `options.groupSortPosition` #356 @yonaskolb
- Added ability to specify `copyFiles` build phase for sources #345 @brentleyjones
- Added ability to specify a `minimumXcodeGenVersion` #349 @brentleyjones
- Added `customArchiveName` and `revealArchiveInOrganizer` to `archive`  #367 @sxua

#### Fixed

- Sort files using localizedStandardCompare #341 @rohitpal440
- Use the latest `xcdatamodel` when sorted by version #341 @rohitpal440
- Fixed compiler flags being set on non source files in mixed build phase target sources #347 @brentleyjones
- Fixed `options.xcodeVersion` not being parsed #348 @brentleyjones
- Fixed non-application targets using `carthage copy-frameworks` #361 @brentleyjones
- Set `xcdatamodel` based on `xccurrentversion` if available #364 @rpassis
- XPC Services are now correctly copied #368 @brentley
- Fixed `.metal` files being added to resources #380 @vgorloff

#### Changed

- Improved linking for `static.library` targets #352 @brentleyjones
- Changed default group sorting to be after files #356 @yonaskolb
- Moved `Frameworks` and `Products` top level groups to bottom #356 @yonaskolb
- `modulemap` files are automatically copied to the products directory for static library targets #346 @brentleyjones
- Public header files are automatically copied to the products directory for static library targets #365 @brentleyjones
- Swift Objective-C Interface Header files are automatically copied to the products directory for static library targets #366 @brentleyjones
- `FRAMEWORK_SEARCH_PATHS` are adjusted for `framework` dependencies #373 @brentley
- `library.static` targets have `SKIP_INSTALL` set to `YES` #358 @brentley
- Copy files phases have descriptive names #360 @brentley

#### Internal

- Moved brew formula to homebrew core
- Added `CONTRIBUTING.md`

## 1.10.3

#### Fixed

- Fixed Mint installations finding `SettingPresets` #338 @yonaskolb

## 1.10.2

#### Changed

- Set `transitivelyLinkDependencies` to false by default

## 1.10.1

#### Fixed

- Fixed `transitivelyLinkDependencies` typo #332 @brentleyjones
- Fixed framework target dependencies not being code signed by default #332 @yonaskolb

#### Changed

- Code sign all dependencies by default except target executables #332 @yonaskolb

## 1.10.0

#### Added

- Added build rule support #306 @yonaskolb
- Added support for frameworks in sources #308 @keith
- Added ability to automatically embed transient dependencies. Controlled with `transitivelyLinkDependencies` #327 @brentleyjones

#### Changed

- Upgraded to Swift 4.1
- Improved Carthage dependency lookup performance with many targets #298 @keith
- By default don't CodeSignOnCopy `target` dependencies. This can still be controlled with `Dependency.codeSign` #324 @yonaskolb

#### Fixed

- Fixed PBXBuildFile and PBXFileReference being incorrectly generated for Legacy targets #296 @sascha
- Fixed required sources build phase not being generated if there are no sources #307 @yonaskolb
- Fixed install script in binary release #303 @alvarhansen
- Removed `ENABLE_TESTABILITY` from framework setting presets #299 @allu22
- Fixed homebrew installation #297 @vhbit
- `cc` files are now automatically recognized as source files #317 @maicki
- Fixed `commandLineArguments` not parsing when they had dots in them #323 @yonaskolb
- Fixed excluding directories that only have sub directories #326 @brentleyjones
- Made `PBXContainerItemProxy` ID more deterministic
- Fixed generated framework schemes from being executable #328 @brentleyjones

## 1.9.0

#### Added

- Scheme pre and post actions can now be added to `target.scheme` #280 @yonaskolb
- Individual files can now be added to `fileGroups` #293 @yonaskolb

#### Changed

- Updated to `xcproj` 4.3.0 for Xcode 9.3 updates
- Update default Xcode version to 9.3 including new settings #284 @LinusU
- **Breaking for ProjectSpec library users** Changed `ProjectSpec` to `Project` and `ProjectSpec.Options` to `SpecOptions`  #281 @jerrymarino

#### Fixed

- Fixed manual build phase of `none` not being applied to folders #288 @yonaskolb
- Quoted values now correctly get parsed as strings #282 @yonaskolb
- Fixed adding a root source folder when `createIntermediateGroups` is on #291 @yonaskolb
- Fixed Homebrew installations issues on some machines #289 @vhbit
- Fixed files that are added as root sources from having invalid parent groups outside the project directory #293 @yonaskolb

## 1.8.0

#### Added

- Added Project `defaultConfig` #269 @keith
- Added Target `attributes` #276 @yonaskolb
- Automatically set `DevelopmentTeam` and `ProvisioningStyle` within `TargetAttributes` if relevant build settings are defined #277 @yonaskolb

#### Fixed

- Fixed default `LD_RUNPATH_SEARCH_PATHS` for app extensions #272 @LinusU

#### Internal

- Make `LegacyTarget` init public #264 @jerrymarino
- Upgrade to _xcproj_ to 4.2.0, _Yams_ to 0.6.0 and _PathKit_ to 0.9.1 @yonaskolb

## 1.7.0

#### Added

- Added support for scheme environment variables #239 @turekj @toshi0383
- Added `carthageExecutablePath` option #244 @akkyie
- Added `parallelizeBuild` and `buildImplicitDependencies` to Schemes #241 @rahul-malik
 @yonaskolb
- Added support for Core Data `xcdatamodeld` files #249 @yonaskolb
- Projects are now generated atomically by writing to a temporary directory first #250 @yonaskolb
- Added script for adding precompiled binary to releases #246 @toshi0383
- Added optional `headerVisibilty` to target source. This still defaults to public #252 @yonaskolb
- Releases now include a pre-compiled binary and setting presets, including an install script

#### Fixed

- Fixed Mint installation from reading setting presets #248 @yonaskolb
- Fixed setting `buildPhase` on a `folder` source. This allows for a folder of header files #254 @toshi0383
- Carthage dependencies are not automatically embedded into test targets #256 @yonaskolb
- Carthage dependencies now respect the `embed` property #256 @yonaskolb
- iMessage extensions now have proper setting presets in regards to app icon and runtime search paths #255 @yonaskolb
- Excluded files are not added within .lproj directories #238 @toshi0383

## 1.6.0

#### Added

- Added scheme pre-actions and post-actions #231 @kastiglione
- Added `options.disabledValidations` including `missingConfigs` to disable project validation errors #220 @keith
- Generate UI Test Target Attributes #221 @anreitersimon

#### Fixed

- Filter out duplicate source files #217 @allu22
- Fixed how `lastKnownFileType` and `explicitFileType` were generated across platforms #115 @toshi0383
- Removed a few cases of project diffs when opening the project in Xcode @yonaskolb
- Fixed Swift not being embedded by default in watch apps @yonaskolb

#### Changed

- Change arrays to strings in setting presets #218 @allu22
- Updated to xcproj 4.0 #227

## 1.5.0

#### Added

- added support for `gatherCoverageData` flag in target schemes #170 @alexruperez
- added support for `commandLineOptions` in target schemes #172 @rahul-malik
- added Project spec as a SwiftPM library for reuse in other projects #164 @soffes
- added `implicit` option for framework dependencies #166 @sbarow
- added `--quite` option to CLI #167 @soffes
- can now print version with `-v` in addition to `--version` #174 @kastiglione
- added support for legacy targets #175 @bkase
- added support for indentation options #190 @bkase
- added source excludes #135 @peymankh @
- added `options.xcodeVersion` #197 @yonaskolb @peymankh
- add test targets to Scheme #195 @vhbit
- add option to make a source file optional incase it will be generated later #200 @vhbit
- finalize Scheme spec #201 @yonaskolb
- added `buildPhase` setting to target source for overriding the guessed build phase of files #206 @yonaskolb
- added `deploymentTarget` setting to project and target #205 @yonaskolb

#### Changed

- huge performance improvements when writing the project file due to changes in xcproj
- updated dependencies
- minor logging changes
- updated Project Spec documentation
- scan for `Info.plist` lazely #194 @kastiglione
- change setting presets so that icon settings only get applied to application targets #204 @yonaskolb
- changed scheme build targets format #203 @yonaskolb
- when specifying a `--spec` argument, the default for the `--project` path is now the directory containing the spec #211 @yonaskolb

#### Fixed

- fixed shell scripts escaping quotes twice #186 @allu22
- fixed `createIntermediateGroups` when using a relative spec path #184 @kastiglione
- fixed command line arguments for test and profile from being overridden #199 @vhbit
- fixed files deep within a hierarchy having the path for a name
- fixed source files from being duplicated if referenced with different casing #212 @yonaskolb
- fixed target product name not being written. Fixes integration with R.swift #213 @yonaskolb

## 1.4.0

#### Added

- added `--version` flag #112 @mironal
- added support for adding individual file sources #106 @bkase
- added source compiler flag support #121 @bkase
- added `ProjectSpec.options.createIntermediateGroups` #108 @bkase
- added better json loading support #127 @rahul-malik
- added source `name` for customizing names of source directories and file #146 @yonaskolb
- added folder reference source support via a new `type` property #151 @yonaskolb
- added `ProjectSpec.options.developmentLanguage` #155 @yonaskolb

#### Changed

- updated to xcproj 1.2.0 #113 @yonaskolb
- build settings from presets will be removed if they are provided in `xcconfig` files #77 @toshi0383
- all files and groups are sorted by type and then alphabetically #144 @yonaskolb
- target sources can now have an expanded form #119 @yonaskolb
- empty build phases are now not generated #149 @yonaskolb
- make UUIDs more deterministic #154 @yonaskolb

#### Fixed

- only add headers to frameworks and libraries #118 @ryohey
- fixed localized files with the same name #126 @ryohey
- fix intermediate sources #144 @yonaskolb
- fix cyclical target dependencies not working #147 @yonaskolb
- fix directory bundles not being added properly when referenced directly #148 @yonaskolb
- made `mm`, `c` and `S` file be parsed as source files #120 @bkase @enmiller
- fix the generation of localized variant groups if there is no `Base.lproj` #157 @ryohey
- all localizations found are added to a projects known regions #157 @ryohey

#### Internal

- refactoring
- more tests
- added release scripts

## 1.3.0

#### Added

- generate output files for Carthage copy-frameworks script #84 @mironal
- added options.settingPreset to choose which setting presets get applied #100 @yonaskolb
- added `link` option for target dependencies #109 @keith

#### Changed

- updated to xcproj 0.4.1 #85 @enmiller
- don't copy base settings if config type has been left out #100 @yonaskolb
- generate localised files under a single variant group #70 @ryohey
- don't apply common project settings to configs with no type #100 @yonaskolb
- config references in settings can now be partially matched and are case insensitive #111 @yonaskolb
- other small internal changes @yonaskolb

#### Fixed

- embed Carthage frameworks for macOS #82 @toshi0383
- fixed copying of watchOS app resources #96 @keith
- automatically ignore more file types for a target's sources (entitlements, gpx, apns) #94 @keith
- change make build to a PHONY task #98 @keith
- allow copying of resource files from dependant targets #95 @keith
- fixed library linking #93 @keith
- fixed duplicate carthage file references #107 @yonaskolb
- an error is now shown if you try and generate a target scheme and don't have debug and release builds @yonaskolb

## 1.2.4

#### Fixed

- setting presets only apply `ALWAYS_EMBED_SWIFT_STANDARD_LIBRARIES: YES` to applications
- don't add carthage dependency to `copy-frameworks` script if `embed: false`
- sort group children on APFS

#### Changed

- update to xcproj 0.3.0

## 1.2.3

#### Fixed

- Fixed wrong carthage directory name reference for macOS #74 @toshi0383
- Removed unnecessary `carthage copy-frameworks` for macOS app target #76 @toshi0383
- Added some missing default settings for framework targets. `SKIP_INSTALL: YES` fixes archiving
- Filter out nulls from setting presets if specifying an empty string

## 1.2.2

#### Added

- automatically set `TEST_TARGET_NAME` on UI test targets if one of the dependencies is an application target

#### Fixed

- set `DYLIB_INSTALL_NAME_BASE` to `@rpath` in framework target presets
- fixed tvOS launch screen setting. `ASSETCATALOG_COMPILER_LAUNCHIMAGE_NAME` is now `LaunchImage` not `tvOS LaunchImage`

## 1.2.0

#### Added

- `include` now supports a single string as well as a list
- add support setting xcconfig files on a project with `configFiles` #64
- add `fileGroups` to project spec for adding groups of files that aren't target source files #64
- better output (more info, emoji, colors)
- add `options.bundleIdPrefix` for autogenerating `PRODUCT_BUNDLE_IDENTIFIER` #67
- add `:REPLACE` syntax when merging `include` #68
- add `mint` installation support

#### Fixed

- fixed homebrew installation
- fixed target xcconfig files not working via `configFiles` #64
- look for `INFOPLIST_FILE` setting in project and xcconfig files before adding it automatically. It was just looking in target settings before #64
- exit with error on failure

## 1.1.0

#### Changed

- set project version to Xcode 9 - `LastUpgradeVersion` attribute to `0900`
- set default Swift version to 4.0 - `SWIFT_VERSION` build setting to `4.0`

### 1.0.1

### Fixed

- fixed incorrect default build script shell path
- fixed install scripts

## 1.0.0

#### Added

- Swift 4 support #52
- Support for C and C++ files #48 by @antoniocasero
- Xcode 9 default settings

#### Fixed

- fixed empty string in YAML not being parsed properly #50 by @antoniocasero

#### Changed

- updated to xcodeproj 0.1.2 #56
- **BREAKING**: changed target definitions from list to map #54

## 0.6.1

#### Added

- Ability to set PBXProject attributes #45

#### Changed

- Don't bother linking target frameworks for target dependencies.
- Move code signing default settings from all iOS targets to iOS application targets, via Product + Platform setting preset files #46

## 0.6.0

#### Added

- Allow a project spec to include other project specs #44

#### Changed

- Changed default spec path to `project.yml`
- Changed default project directory to the current directory instead of the spec file's directory

## 0.5.1

#### Fixed

- Fix embedded framework dependencies
- Add `CODE_SIGN_IDENTITY[sdk=iphoneos*]` back to iOS targets
- Fix build scripts with "" generating invalid projects #43

## 0.5.0

#### Added

- Added multi platform targets #35
- Automatically generate platform specific `FRAMEWORK_SEARCH_PATHS` for Carthage dependencies #38
- Automatically find Info.plist and set `INFOPLIST_FILE` build setting if it doesn't exist on a target #40
- Add options for controlling embedding of dependencies #37

#### Fixed

- Fixed localized files not being added to a target's resources

#### Changed

- Renamed Setting Presets to Setting Groups
- Carthage group is now created under top level Frameworks group

## 0.4.0

##### Added

- Homebrew support #16 by @pepibumur
- Added `runOnlyWhenInstalling` to build scripts #32
- Added `carthageBuildPath` option #34

#### Fixed

- Fixed installations of XcodeGen not applying build setting presets for configs, products, and platforms, due to missing resources

#### Changed

- Upgraded to <https://github.com/swift-xcode/xcodeproj> 0.1.1 #33

## 0.3.0 - Extensions and Scheme Tests

#### Added

- Support for app extension dependencies, using the same `target: MyExtension` syntax #19
- Added test targets to generated target schemes via `Target.scheme.testTargets` #21

#### Changed

- Updated xcodeproj to 0.0.9

#### Fixed

- Fixed watch and messages apps not copying carthage dependencies

#### Breaking changes

- Changed `Target.generatedSchemes` to `Target.scheme.configVariants`

## 0.2.0 - Build scripts

#### Added

- Added Target build scripts with `Target.prebuildScripts` and `Target.postbuildScripts` #17
- Support for absolute paths in target sources, run script files, and config files
- Add validation for incorrect `Target.configFiles`

#### Fixed

- Fixed some project objects sometimes having duplicate ids

## 0.1.0

First official release
