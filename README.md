# CloudFront origin-facing IPv4 ranges

`cloudfront-origin-facing-v4.txt` lists every IPv4 prefix that AWS publishes for the
`CLOUDFRONT_ORIGIN_FACING` service in <https://ip-ranges.amazonaws.com/ip-ranges.json>:
the addresses CloudFront uses to connect to an origin. One CIDR per line, sorted by
address, no header and no comments, so a UniFi External Network List can read it as is.

`source.txt` records the AWS `syncToken` and `createDate` the list was taken from.

A daily job on docker-vm-1 (`/opt/scripts/cloudfront-origin-ips.py`) refreshes it and
commits only when the list changes. It refuses to publish if the fetch fails, a line is
not a valid IPv4 CIDR, or the count falls outside 30 to 150, so a bad AWS response
leaves the last good list in place.
