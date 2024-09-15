
# What are Con jobs?

Cron jobs are used to schedule tasks to run periodically at fixed times, dates, or intervals. They are commonly used to automate system maintenance or administration tasks, such as backing up files, updating software packages, monitoring system resources, or generating reports. A very practical use outside of general sysadmin tasks would be to run a python script that loads CSV files or scrapes a website for data, which then uses that data to generate a report that could be emails to a user or saved to a file. 

While cron jobs are a powerful tool, we must refrain from using them for the following:

- Running tasks that require user input
- Running tasks that require a GUI
- **Real-time processing:** tasks that require immediate processing or response
- **frequent tasks that require sub-minute intervals:** the minimum interval for a cron job is 1 minute so tasks that require sub-minute intervals should have their own dedicated process or service
- **complex tasks that require a lot of dependencies:** for some tasks you will need a particular order a range of processes need to run in. These can vary and can require multiple checks and potential re-runs. While there is nothing stopping you from doing this in a cron job, tools like `make` and `Jenkins` will be much better suited for these tasks.
- **event driven tasks:** these tasks generally require listening to specific events constantly to react to meaning that they require a dedicated service or process to run.

Now that we know what cron jobs are used for, we can move onto how cron jobs work.

# How do cron jobs work?

Cron jobs operate as part of the `cron` daemon, a background process in Unix-like operating systems that schedules and executes tasks based on predefined time intervals specified by users in crontab files. The `cron` daemon runs continiously in the background checking the crontab files for tasks to run. Cron tabs are instructions and times for the cron daemon to run tasks. Each tab is a task to be run. On most systems, there is a file for system tasks, and a file for user tasks. An example of a user cron file is shown below:

```bash
# 1. Run a backup script every day at 2:30 AM
30 2 * * * /usr/local/bin/backup.sh

# 2. Clean temporary files every Sunday at 5:00 AM
0 5 * * 0 /usr/local/bin/cleanup_temp_files.sh

# 3. Sync files to a remote server every 15 minutes
*/15 * * * * /usr/local/bin/sync_files.sh

# 4. Send a report via email every Monday at 7:00 AM
0 7 * * 1 /usr/local/bin/send_report.sh

# 5. Run a Python script that requires input every day at 10:00 AM
0 10 * * * /usr/bin/python3 /usr/local/bin/generate_report.py <<EOF
input1
input2
input3
EOF
```
 We can go through each task in the above example:

### Task 1:
Runs a backup script daily at 2:30 AM
`30 2 * * *` means minute 30, hour 2, every day of the month, every month, and every day of the week.

### Task 2:
Cleans temporary files every Sunday at 5:00 AM
`0 5 * * 0` means minute 0, hour 5, every day of the month, every month, and Sunday (0 represents Sunday in cron).

### Task 3:
Syncs files to a remote server every 15 minutes
`*/15 * * * *` means every 15 minutes, every hour, every day of the month, every month, and every day of the week.

### Task 4:
Sends a report via email every Monday at 7:00 AM
`0 7 * * 1` means minute 0, hour 7, every day of the month, every month, and Monday (1 represents Monday in cron).

### Task 5:
Runs a Python script that requires input every day at 10:00 AM
`0 10 * * *` means minute 0, hour 10, every day of the month, every month, and every day of the week. The `<<EOF` and `EOF` syntax is a here document in Bash, which allows you to pass multiple lines of input to a command.

Now that we understand how cron jobs work, we can move onto how to create a cron job.

# How to create a cron job?

In this section, we are going to create a basic cron job that echoes a message to a file every minute. First, we must create the script with the following command:

```bash
sudo touch /usr/local/bin/backup.sh
```

We are putting the script in `/usr/local/bin` as it is a common location for user scripts. You need extra permissions, however, binaries, and scripts in this location are available in your terminal directly. For instance, if we has a binary or script called `test`, everytime we typed `test` into our terminal, it would run the script or binary. If you look inside your `/usr/local/bin`, you will see binaries and scripts that are the same name as the command you run in your terminal. For instance, if you have docker installed, you will see a binary called `docker` in `/usr/local/bin`.

Inside our script we will add the following code:

```bash
echo "Hello Cron!"
```

We now must ensure that the script is executable with the correct permissions with the following command:

```bash
sudo chmod +x /usr/local/bin/backup.sh
```

We can now edit the crontab file for the cron daemon with the following command:

```bash
crontab -e
```

This will open the crontab file in a default editor like `nano` or `vim`. We can now add the following line to the file:

```bash
* * * * * sh /usr/local/bin/backup.sh
```
This means we will run our script every minute. If we have opened the crontab file in `vim`, you must then press `esc` and type `:wq`, and then enter to save and exit the file. If you have opened the file in `nano`, you must press `ctrl + x` and then `y` to save and exit the file. Once you have exited, you might get a permissions alert depending on your system. This is because the cron daemon needs to reload the crontab file. You can ok this alert and the cron daemon will reload the crontab file. Once this is done, you will then get the confirmation that the cron job has been added. You can check this by running the following command:

```bash
crontab -l
```

Which will list all the cron jobs in the crontab file. You should see the following output:

```bash
* * * * * /usr/local/bin/backup.sh
```

Due to the nature of the cron jobs will will now have to wait five minutes or so to allow the background tasks to run multiple times. For me, I went and did something else, came back to my computer, and typed in the following command:

```bash
mail
```

This gave me the following output:

```bash
"/var/mail/maxwellflitton": 11 messages 11 new
>N  1 maxwellflitton@maxwe  Sun Sep 15 10:12  18/708   "Cron <maxwellflitton@maxwells-mbp> sh /usr/local/bin/backup.sh"
 N  2 maxwellflitton@maxwe  Sun Sep 15 10:13  18/708   "Cron <maxwellflitton@maxwells-mbp> sh /usr/local/bin/backup.sh"
 N  3 maxwellflitton@maxwe  Sun Sep 15 10:13  18/708   "Cron <maxwellflitton@maxwells-mbp> sh /usr/local/bin/backup.sh"
 N  4 maxwellflitton@maxwe  Sun Sep 15 10:14  18/708   "Cron <maxwellflitton@maxwells-mbp> sh /usr/local/bin/backup.sh"
 N  5 maxwellflitton@maxwe  Sun Sep 15 10:15  18/708   "Cron <maxwellflitton@maxwells-mbp> sh /usr/local/bin/backup.sh"
 N  6 maxwellflitton@maxwe  Sun Sep 15 10:16  18/708   "Cron <maxwellflitton@maxwells-mbp> sh /usr/local/bin/backup.sh"
```

Here, we can see that the cron daemon has executed the jobs, and sent the outcome of the jobs to my mail client. If we press enter, we will start going through the messages and see the output of the cron job which should look like the following:

```bash
Message 1:
From maxwellflitton@maxwells-mbp.lan  Sun Sep 15 10:12:00 2024
X-Original-To: maxwellflitton
Delivered-To: maxwellflitton@maxwells-mbp.lan
From: maxwellflitton@maxwells-mbp.lan (Cron Daemon)
To: maxwellflitton@maxwells-mbp.lan
Subject: Cron <maxwellflitton@maxwells-mbp> sh /usr/local/bin/backup.sh
X-Cron-Env: <SHELL=/bin/sh>
X-Cron-Env: <PATH=/usr/bin:/bin>
X-Cron-Env: <LOGNAME=maxwellflitton>
X-Cron-Env: <USER=maxwellflitton>
Date: Sun, 15 Sep 2024 10:12:00 +0100 (BST)

Hello Cron!
```

If you continue to press enter, you will go through the other messages until there are none left. We can remove our cron job by deleting the line from the crontab file and saving the file. We can then check the crontab file with the `crontab -l` command to ensure the job has been removed.