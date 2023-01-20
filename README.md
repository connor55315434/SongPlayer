# SongPlayer
A Fabric mod for Minecraft that plays songs with noteblocks.
The current version is for Minecraft 1.19.x.

# How to install
You can grab the mod jar from releases section.
This mod requires fabric api.

# Adding songs
You can put midis or NoteBlockStudio files in the `.minecraft/songs` folder.
SongPlayer supports any valid midi and all versions of NBS files.

# Using the client
To get started, add some midis or nbs files to your songs folder, and use `$play <filename>` in an open area.
If you have provided it a valid midi or nbs file, it will either:
try to set your gamemode to creative, place the required noteblocks for the song, try to switch you to survival, then start playing. OR:
try to play the song using only commands such as /playsound depending on your settings.

# Commands
All the commands are not case-insensitive.

### $help
Lists all SongPlayer commands

### $help \<command>
Explains a command and shows the command usage.

### $play \<filename or url>
Plays a particular midi from the .minecraft/songs folder, or, if a url is specified, downloads the song at that url and tries to play it.

If there is a song already playing, the new song will be added to the queue.

### $playlist \<create, delete, play> <playlist name> OR: $playlist \<sort> <addedfirst, alphabetically, shuffle> OR: $playlist \<edit> \<playlist name> \<add, remove> \<song>
Manage or play a list of songs

### $prefix <prefix>
Sets the command prefix used to execute these commands.
Example: `$prefix !` will change commands to `!example command` instead of `$example command`

### $toggle <swing, rotate, useCommandsToPlay> <false, true>
Toggles certain features I added as ideas when forking this. All are toggled to false by default.
- Swing: weather you swing your hand when you play a noteblock
- Rotate: weather you rotate to the noteblock you are placing / playing
- useCommandsToPlay: weather you should use commands to play instead of noteblocks

### $stop
Stops playing/building and clears the queue or playlist.

### $skip
Skips the current song and goes to the next one in the queue or playlist.

### $goto \<mm:ss>
Goes to a specific time in the song.

### $loop
Toggles song looping.

### $status
*aliases: `$current`*

Gets the status of the current song that is playing.

### $queue
*aliases: `$showqueue`*

Shows all the songs in the queue or playlist.

### $songs
*aliases: `$list`*

Lists the songs in your .minecraft/songs folder.

### $setCommand <creative, survival, playnote, displayprogress> \<command>
Changes what command is used for certain circumstances.

### $setCreativeCommand \<command>
*aliases: `$sc`*

Shortcut for `$setCommand creative`
For example, if the server uses vanilla commands, do `$setCreativeCommand /gamemode creative`.

### $setSurvivalCommand \<command>
*aliases: `$ss`*

Shortcut for `$setCommand survival`
For example, if the server uses vanilla commands, do `$setSurvivalCommand /gamemode survival`.

### $useVanillaCommands
*aliases: `$essentials`, `$useEssentials`, `$essentialsCommands`*

Switch to using Essentials gamemode commands.

Equivalent to `$setCommand creative /gmc` and `$setCommand survival /gms`

### $useVanillaCommands
*$aliases: `$vanilla`, `$useVanilla`, `$vanillaCommands`*

Switch to using vanilla gamemode commands.

Equivalent to `$setCommand creative /gamemode creative` and `$setCommand survival /gamemode survival`

### $toggleFakePlayer
*aliases: `$fakePlayer`, `$fp`*

Toggles whether a fake player will show up to represent your true position while playing a song. When playing a song, since it automatically enables freecam, your true position will be different from your apparent position. The fake player will show where you actually are. By default, this is disabled.

### $testSong
A command I used for testing during development.
It plays every single noteblock sound possible in order.
However, there are 400 possible noteblocks but the max stage size is 300, so that last 100 notes aren't played.

# Mechanism
--- using noteblocks ---
SongPlayer places noteblocks with nbt and instrument data already in them, so the noteblocks do not need to be individually tuned. Ayunami2000 has previously done a proof-of-concept of this method.

My client will automatically detect what noteblocks are needed and place them automatically before each song is played, which makes playing songs quite easy. The only drawback is that you need to be able to switch between creative and survival mode, which my client will attempt to do automatically.

When playing a song, freecam is enabled. You will be able to move around freely, but in reality you are only moving your camera while your player stays at the center of the noteblocks. This is because noteblocks can only be played if you're within reach distance of them, so you have to stand at the center of the noteblocks to play them, but it's still nice to be able to move around while your song is playing.

--- using commands ---
SongPlayer will use commands such as /execute and display progress for everyone with /title by default.

This will only work if you have op on a minecraft server, and some servers may kick you for spamming.

Use this mode with caution.
