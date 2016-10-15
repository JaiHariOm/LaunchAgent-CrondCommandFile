### localhost.brew-file.updatede.plist

* 実行後、通知センターで知らせるよう設定

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
	<key>Label</key>
	<string>localhost.brew-file.updatede</string>
	<key>ProcessType</key>
	<string>Background</string>
	<key>ProgramArguments</key>
	<array>
		<string>/bin/zsh</string>
		<string>-c</string>
		<string>/usr/local/bin/brew-file --leaves update &amp;&amp; /usr/local/bin/terminal-notifier -title 'BrewFile' -message 'brew file update'</string>
	</array>
	<key>RunAtLoad</key>
	<true/>
	<key>StartCalendarInterval</key>
	<array>
    <dict>
        <key>Hour</key>
        <integer>12</integer>
        <key>Minute</key>
        <integer>2</integer>
    </dict>
    <dict>
        <key>Hour</key>
        <integer>18</integer>
        <key>Minute</key>
        <integer>2</integer>
    </dict>
    <dict>
        <key>Hour</key>
        <integer>23</integer>
        <key>Minute</key>
        <integer>2</integer>
    </dict>
	</array>
		<key>StandardErrorPath</key>
		<string>/tmp/localhost.brew-file.updatede.stderr</string>
		<key>StandardOutPath</key>
		<string>/tmp/localhost.brew-file.updatede.stdout</string>
</dict>
</plist>
```

### localhost.brew.cask.upgrade.plist

* 実行後、通知センターで知らせるよう設定

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
	<key>Label</key>
	<string>localhost.brew.cask.upgrade</string>
	<key>ProcessType</key>
	<string>Background</string>
	<key>ProgramArguments</key>
	<array>
		<string>/bin/zsh</string>
		<string>-c</string>
		<string>/usr/local/bin/brew cask upgarade -C &amp;&amp; /usr/local/bin/terminal-notifier -title 'Brew Cask Upgrader' -message 'Cask upgraded!'</string>
	</array>
	<key>StartCalendarInterval</key>
	<dict>
		<key>Weekday</key>
    <integer>1</integer>
    <key>Hour</key>
    <integer>19</integer>
    <key>Minute</key>
    <integer>1</integer>
 	</dict>
		<key>StandardErrorPath</key>
		<string>/tmp/localhost.brew.cask.upgrade.stderr</string>
		<key>StandardOutPath</key>
		<string>/tmp/localhost.brew.cask.upgrade.stdout</string>
</dict>
</plist>
```

### rsync の設定 me.Test.rsync.plist

* rsync での同期、コピー、変更追記テスト用に、元ディレクトリ → 指定ディレクトリを指定して試してみた
    
```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
    <dict>
        <key>Label</key>
        <string>me.Test.rsync</string>
        <key>ProgramArguments</key>
        <array>
            <string>rsync</string>
            <string>-au</string>
            <string>--delete</string>
            <string>/Users/home/workspace/RSync-Launchd-Log/TestText_WorkingSpeace</string>
            <string>/Users/home/workspace/RSync-Launchd-Log/TestTextLog</string>
        </array>
        <key>StandardOutPath</key>
        <string>/tmp/me.Test.rsync.monitor.out.log</string>
        <key>StandardErrorPath</key>
        <string>/tmp/me.Test.rsync.monitor.err.log</string>
        <key>WatchPaths</key>
        <array>
            <string>/Users/home/workspace/RSync-Launchd-Log/TestText_WorkingSpeace</string>
        </array>
    </dict>
</plist>
```

### rsync の設定 Log.LaunchAgenr.rsync.plist

* brew file の実行結果の log を指定ディレクトリへ sync する (追加コピー)
    
    
```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
    <dict>
        <key>Label</key>                                                                                                                                                                   
        <string>Log.LaunchAgent.rsync</string>
        <key>ProgramArguments</key>
        <array>
            <string>rsync</string>
            <string>-auv</string>
            <string>--delete</string>
            <string>/private/tmp/localhost.brew-file.updatede.stdout</string>
            <string>/Users/home/workspace/RSync-Launchd-Log/Brew_File_Log</string>
        </array>
        <key>StandardOutPath</key>
        <string>/tmp/Log.LaunchAgent.rsync.monitor.out.log</string>
        <key>StandardErrorPath</key>
        <string>/tmp/Log.LaunchAgent.rsync.monitor.err.log</string>
        <key>WatchPaths</key>
        <array>
            <string>/private/tmp</string>
        </array>
    </dict>
</plist>
```