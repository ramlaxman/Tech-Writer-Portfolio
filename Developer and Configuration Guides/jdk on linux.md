1. Log in as root from terminal

2. Create file as follows:
   gedit ~/.bashrc

3. Edit the following text:
   export PATH=/usr/lib/jvm/jdk1.7.0_45/bin:$PATH

4. Edit the ~/.profile

   only this part if not present
   if [ -n "$BASH_VERSION" ]; then
      # include .bashrc if it exists
      if [ -f "$HOME/.bashrc" ]; then
	. "$HOME/.bashrc"
      fi
   fi

5. Now restart the terminal.

6. Check with javac if any help commands are appearing means JDK has added to PATH.

 


