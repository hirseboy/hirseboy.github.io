---
title: Managing Flatpak Applications and Checking Sizes
date: 2026-01-26 12:00:00
categories: [linux, flatpak]
tags: [flatpak, package-management, disk-usage, linux]
---

# Flatpak Application Management

Flatpak is a universal package manager for Linux that allows you to distribute applications independent of the Linux distribution. One useful aspect of managing flatpak applications is being able to view installed applications and their disk usage.

## Listing Flatpak Applications

To view all installed flatpak applications with their sizes, use the following command:

```bash
flatpak list --columns=application,size
```

This command displays a table with two columns:
- **application**: The application ID or name of the installed flatpak
- **size**: The disk space used by each application

### Understanding the Output

The output will look similar to this:

```
Application                          Size
org.gnome.Evolution                  250.0 MB
org.mozilla.firefox                  420.3 MB
com.github.tchx84.Flatseal          12.5 MB
org.gnome.Extensions                 8.2 MB
```

## Other Useful Flatpak List Commands

You can customize the output with different column options:

### Show all available information
```bash
flatpak list --app --columns=application,version,branch,origin,size
```

### Only system flatpaks
```bash
flatpak list --app --system
```

### Only user flatpaks
```bash
flatpak list --app --user
```

### Show runtimes
```bash
flatpak list --runtime
```

## Managing Flatpak Storage

To see detailed information about flatpak storage usage:

```bash
du -sh ~/.var/app/*/
```

This shows the size of data directories for each installed application in your home directory.

## Cleaning Up Unused Flatpaks

To remove unused flatpaks and free up disk space:

```bash
# Remove unused runtimes
flatpak uninstall --unused

# Remove a specific application
flatpak uninstall org.mozilla.firefox

# Remove unused data
flatpak repair
```

## Summary

Flatpak's `list` command with various column options provides a convenient way to monitor your installed applications and their resource usage. This is particularly useful when managing storage on systems with limited disk space or when auditing which flatpaks are installed.
