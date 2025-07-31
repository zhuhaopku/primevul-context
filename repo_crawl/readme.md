# PrimeVul Context Extraction - Repository Crawling Stage

## Overview

During the processing of the PrimeVul test dataset, we encountered a large variety of Git commit URLs in different formats that needed to be parsed and mapped to cloneable repository addresses. Through systematic analysis and iterative optimization, we achieved a 100% URL parsing success rate.

## Dataset Statistics

- **Total samples**: 870
- **Unique repositories(commit-specific)**: 423  
- **Supported URL formats**: 15+

## Main Challenges & Solutions

### 1. GitHub Standard Format ✅
```
https://github.com/owner/repo/commit/hash
```
**Solution**: Direct regex matching, no conversion needed

### 2. Git Web Interface Format ✅
```
http://git.qemu.org/?p=qemu.git;a=commit;h=hash
```
**Solution**: Map to corresponding GitHub mirror repositories

### 3. Kernel.org Multiple CGit Formats ✅
```
https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=hash
https://git.kernel.org/cgit/linux/kernel/git/davem/net.git/commit/?id=hash
```
**Solution**: Unified mapping to Linux mainline kernel repository

### 4. GitLab and Merge Request Formats ✅
```
https://gitlab.freedesktop.org/cairo/cairo/-/commit/hash
https://gitlab.freedesktop.org/cairo/cairo/-/merge_requests/85/diffs?commit_id=hash
```
**Solution**: Map to GitHub mirrors or maintain original GitLab addresses

### 5. Various Git Hosting Platform Special Formats ✅

**Bitbucket**
```
https://bitbucket.org/tildeslash/monit/commits/hash
```

**Tor Project Gitweb**
```
https://gitweb.torproject.org/tor.git/commitdiff/hash
```

**Direct Git Repositories**
```
http://git.exim.org/exim.git/commit/hash
https://git.lysator.liu.se/nettle/nettle/commit/hash
```

### 6. GNU Project Multiple Formats ✅
```
https://git.savannah.gnu.org/cgit/gnulib.git/commit/?id=hash
https://git.sv.gnu.org/cgit/grep.git/commit/?id=hash
```
**Solution**: Map to official GNU GitHub mirrors

### 7. Open Source Project Proprietary Git Interfaces ✅
```
https://git.clamav.net/gitweb?p=clamav-devel.git;a=commit;h=hash
https://git.libssh.org/projects/libssh.git/commit/?id=hash
https://git.openssl.org/gitweb/?p=openssl.git;a=commitdiff;h=hash
```
**Solution**: Individual analysis and mapping to corresponding GitHub repositories

## Technical Implementation

### Parsing Strategy

1. **Regex Pattern Matching**: Create specialized regex patterns for each URL format
2. **Priority Ordering**: Sort by frequency, prioritizing standard formats like GitHub
3. **Repository Mapping**: Unify various Git hosting platform URLs to GitHub mirrors
4. **Incremental Optimization**: Iteratively improve parsing rules by analyzing failure cases

## Key Features

- **100% Success Rate**: All 870 samples successfully parsed and mapped
- **Comprehensive Coverage**: Supports 15+ different URL formats from various platforms
- **Robust Mapping**: Intelligent repository mapping to ensure accessibility
- **Scalable Architecture**: Easy to extend for new URL formats

## Usage

This crawling stage serves as the foundation for extracting relevant context from the PrimeVul pair test dataset, ensuring all repository URLs are properly parsed and accessible for subsequent analysis.
