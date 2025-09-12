# Downloading DBveaver
Installing **DBeaver on macOS**. You have a couple of options: **using a DMG installer** or **using Homebrew**.

The following are the steps for installing DBveaver on Macos.


### **Method 1: Download DMG (manual install)**

1. Go to the [DBeaver official download page](https://dbeaver.io/download/).
2. Choose **macOS (Intel / ARM depending on your Mac)**.
3. Download the `.dmg` file.
4. Open the `.dmg` file and drag **DBeaver.app** to your **Applications** folder.
5. Open DBeaver from **Applications**.



### **Method 2: Install via Homebrew**

1. Make sure Homebrew is installed. If not, run in Terminal:

   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```

2. Install DBeaver using Homebrew:

   ```bash
   brew install --cask dbeaver-community
   ```

3. Launch DBeaver:

   ```bash
   open /Applications/DBeaver.app
   ```

---