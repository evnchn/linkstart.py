# linkstart.py

Easy auto-installation of dependencies for smooth script start. Minimal migration is needed. 

## Usage

Begin your scripts with
```py
import_string = \
'''
[insert import statements here]
'''
```

Move all import statements to the `[insert import statements here]` section

For special dependencies whose name does not equal that in the import statement, simply put the name after `#`, such as

```py
import_string = \
'''
from bs4 import BeautifulSoup # beautifulsoup4
import discord # discord.py
'''
```

Right after that, paste the following:
```py
### LINK START! (https://github.com/evnchn/linkstart.py)
for line in import_string.splitlines():
    if "import" in line:
        print(line)
        try:
            exec(line)
        except:
            if "#" in line:
                package_name = line.split("#")[-1]
            else:
                splits = line.split("import")
                if "from" in line:
                    package_name = splits[0].replace("from","")
                else:
                    package_name = splits[1]
            package_name = package_name.strip()
            print("Installing {}...".format(package_name))    
            import subprocess
            import sys
            subprocess.check_call([sys.executable, "-m", "pip", "install", package_name])
            try:
                exec(line)
            except:
                print("Failed to install {}".format(package_name))
### DONE
```

Everything should _just work_ when you run the script next time. 

## Sample

Please refer to `linkstart.py`
