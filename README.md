### How to make programmer life a little lazier ? 😉
You are probably using git commands to version control your project, but typing all these three commands 
### (git add, git commit, git push) 
again and again is boring and time consuming, So I use this single command *gap*

- How to combine all three "git add",  "git commit -m" and "git push" command and access this function from command line.

### In Linux 🐚 or Mac 🍎 Add below function to your  `~/.bash_profile` file.

```bash
gap() {
	if [ -z "$1" ]; then
		echo "Error: Commit message is required."
		return 1
	fi

	commit_message="$1"
	shift

	if [ -z "$1" ]; then
		echo "Error: At least one file is required."
		return 1
	fi

	git add "$@" && git commit -m "$commit_message" && git push
}
```

### Follow below steps in Windows 🪟 to Add below function in PowerShell `profile.ps1` file.

- Create a new profile file

```powershell
New-Item -ItemType File -Path $Profile -Force
```

- Open the profile file

```powershell
notepad $Profile
```

Paste below code to notepad

```powershell
Function gap {
	if (-not $args[0]) {
		Write-Error "Error: Commit message is required."
		return 1
	}

	$commit_message = $args[0]
	$files = $args[1..$args.Length]

	if (-not $files) {
	    Write-Error "Error: At least one file is required."
	    return 1
	}

	git add $files; git commit -m "$commit_message"; git push
}
```

```powershell
Get-ExecutionPolicy
Set-ExecutionPolicy RemoteSigned
```

- Reload the profile file for the changes to take effect

```powershell
. $profile
```
