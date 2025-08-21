# Sanad Cleanup & Reindexing – SQL Automation

This project provides a robust SQL script to clean up orphaned سند records and reindex No_Sanad values for year 1404 in accounting systems.

## Features
- Detects and deletes orphaned سندs in Hsb_Bod_Sanad
- Reindexes سند numbers to maintain continuity
- Fully dynamic range detection using MIN/MAX
- Safe and production-ready logic

## Usage
Run cleanup_sanad.sql in your SQL Server environment. Make sure to back up your data before execution.

## Snippets
See [snippets/sanad_reindexing_snippet.txt](snippets/sanad_reindexing_snippet.txt) for a professional summary.
