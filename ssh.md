# SSH

`subsystem request failed on channel 0`

Use -O to force old compatibility sftp protocol

    `scp -p -O -P ...`

for servers that do not understand the new one.

# FAQ

### Issue: scp does not connect while ssh does `Connection closed`.

Note: Since OpenSSH 8.8 the scp utility uses the SFTP protocol by default.
The `-O` option must be used to use the legacy SCP protocol.
