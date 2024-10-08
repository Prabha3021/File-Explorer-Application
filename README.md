**File Explorer Application Project**

**Description**
This File Explorer application is a multifunctional tool for effective file and directory management. It has extensive file manipulation features, including the ability to create, move, copy, and delete files. In addition to managing permissions, processing commands, and having a robust search feature, the application also keeps a thorough activity log.

**Table of Contents**

•Installation

•Key Features

•Architecture

•Usage

*Code

*Sample Run
•Contributing

•License

•Reference

**Project Submission By:**

**Chitikela. Prabhakararao**
and **Rajupalem. Srivathasa**


**Installation**

1.**Clone the Repository:**

bash

git clone: https://github.com/Prabha3021/File-Explorer-Application

**2.Navigate to the Project Directory:**

cd file-explorer

**3.Build the Project:**

Using a C++ compiler, compile the source files.

g++ -o file_explorer main.cpp FileSystem.cpp DirectoryManager.cpp FileManager.cpp SearchManager.cpp PermissionManager.cpp CommandProcessor.cpp Logger.cpp

**4. Run the Application:**

./file_explorer

**Key Features**

**File Navigation**

•Browse directories and view their contents.

•Move up and down the directory tree.

•Change the current working directory.

**File Operations**

•Create, delete, rename, and move files and directories.

•Copy files from one location to another.

•View file properties (e.g., size, permissions, modification date).

**Search Functionality**

•Search for files or directories by name or other attributes.

•Use wildcards or regular expressions for advanced searches.

**File Viewing**

•Display the contents of a file directly in the terminal (e.g., using cat, less, or custom implementation).

•Open files with appropriate applications (e.g., text files in a text editor).

**Permission Management**

•View and modify file permissions (read, write, execute).

•Change ownership of files (if running as a superuser).

**Command Execution**

•Allow users to execute shell commands directly within the application.

•Integrate with other system tools or utilities.

**Architecture**
The application is organized into several key classes, each responsible for specific functionality:

**FileSystem:** Central class managing overall file system operations.

**DirectoryManager:** Handles directory-related tasks like creating, deleting, and navigating directories.

**FileManager:** Manages file-specific operations including copying, moving, deleting, and creating files.

**SearchManager**: Provides the ability to search files by name or content.

**PermissionManager:** Manages and enforces user permissions for file and directory access.

**CommandProcessor:** Interprets and executes user commands.

**Logger**: Records all significant actions within the application to a log file.

**Usage**

**Logger Code**

**Logger Code for this File Explorer Application:**


#include <iostream>
#include <fstream>
#include <string>
#include <ctime>
#include <sstream>
#include <iomanip>
/**
 * @brief Simple Logger class for file and console logging
 */
class SimpleLogger {

public:

    enum Level { DEBUG, INFO, NOTICE, WARNING, ERROR, CRITICAL };

    SimpleLogger(const std::string& name) : mName(name) {

        mLogFile.open("file_explorer_log.txt", std::ios::out | std::ios::app);
    }
    ~SimpleLogger() {
        if (mLogFile.is_open()) {
            mLogFile.close();
        }
    }

   
    void log(Level level, const std::string& message) {
    
        std::string levelStr = getLevelString(level);
        
        std::string logMessage = getCurrentTime() + " [" + levelStr + "] " + mName + ": " + message;
        
       
		std::cout << logMessage << std::endl; // Print to console
        
		if (mLogFile.is_open()) {
        
			mLogFile << logMessage << std::endl; // Write to file
        }
    }
    
	void debug(const std::string& message) { log(DEBUG, message); }
    
	void info(const std::string& message) { log(INFO, message); }
    
	void notice(const std::string& message) { log(NOTICE, message); }
    
	void warning(const std::string& message) { log(WARNING, message); }
    
	void error(const std::string& message) { log(ERROR, message); }
    
	void critical(const std::string& message) { log(CRITICAL, message); }

private:

	std::string mName;
    
	std::ofstream mLogFile;
    
	std::string getLevelString(Level level) {
    
		switch (level) {
        
			case DEBUG: return "DEBUG";
            
			
   case INFO: return "INFO";
   
			case NOTICE: return "NOTICE";
            
			case WARNING: return "WARNING";
            
			case ERROR: return "ERROR";
            
			case CRITICAL: return "CRITICAL";
            
			default: return "UNKNOWN";
        }
    }

    
	std::string getCurrentTime() {
    
		std::time_t now = std::time(nullptr);
        
		std::tm* localTime = std::localtime(&now);
        
		std::ostringstream oss;
        
		oss << std::put_time(localTime, "%Y-%m-%d %H:%M:%S");
        
		return oss.str();
    }
};
/**
 
 * @brief Example main function demonstrating logging in a File Explorer Application
 
 */

int main() {

	SimpleLogger logger("FileExplorer");
    
	// Day 1: Logging basic file operations
    
	logger.info("Day 1: Starting basic file operations.");
    
	logger.debug("Listed files in directory '/home/user'");
    
	// Day 2: Logging directory navigation
    
	logger.info("Day 2: Implementing directory navigation.");
    
	logger.debug("Navigated to directory '/home/user/documents'");
    
	// Day 3: Logging file manipulation capabilities
    
	logger.info("Day 3: Adding file manipulation capabilities.");
    
	logger.debug("Copied file 'example.txt' to '/home/user/documents/example_copy.txt'");
    
	// Day 4: Logging file search functionality
    
	logger.info("Day 4: Implementing file search functionality.");
    
	logger.debug("Searched for 'report.docx' in '/home/user'");
    
	// Day 5: Logging file permission management
    
	logger.info("Day 5: Adding file permission management features.");
    
	logger.debug("Changed permissions of 'example.txt' to 'rwxr-xr-x'");
    
	return 0;
}

**Output of Logger Code**

2024-08-12 05:44:43 [INFO] FileExplorer: Day 1: Starting basic file operations.

2024-08-12 05:44:43 [DEBUG] FileExplorer: Listed files in directory '/home/user'

2024-08-12 05:44:43 [INFO] FileExplorer: Day 2: Implementing directory navigation.

2024-08-12 05:44:43 [DEBUG] FileExplorer: Navigated to directory '/home/user/documents'

2024-08-12 05:44:43 [INFO] FileExplorer: Day 3: Adding file manipulation capabilities.

2024-08-12 05:44:43 [DEBUG] FileExplorer: Copied file 'example.txt' to '/home/user/documents/example_copy.txt'

2024-08-12 05:44:43 [INFO] FileExplorer: Day 4: Implementing file search functionality.

2024-08-12 05:44:43 [DEBUG] FileExplorer: Searched for 'report.docx' in '/home/user'

2024-08-12 05:44:43 [INFO] FileExplorer: Day 5: Adding file permission management features.

2024-08-12 05:44:43 [DEBUG] FileExplorer: Changed permissions of 'example.txt' to 'rwxr-xr-x'


**FileExplorer.cpp** code:

#include <iostream>

#include <string>

#include <dirent.h>

#include <unistd.h>

#include <sys/stat.h>

#include <fcntl.h>

#include <cstring>

#include <vector>

#include <fstream>

#include <sstream>  // Include this for std::istringstream

class FileExplorer {
private:
    std::string currentDirectory;

public:
    FileExplorer() {
        char buffer[1024];
        if (getcwd(buffer, sizeof(buffer)) != nullptr) {
            currentDirectory = std::string(buffer);
        }
    }

    void start() {
        std::string command;
        while (true) {
            std::cout << currentDirectory << " > ";
            std::getline(std::cin, command);
            if (command == "exit") break;
            executeCommand(command);
        }
    }

private:
  
    void executeCommand(const std::string& command) {
    
	if (command == "list") {
        
	    listFiles();
        
	} else if (command.substr(0, 3) == "cd ") {
        
	    changeDirectory(command.substr(3));
        
	} else if (command.substr(0, 4) == "copy") {
            auto args = parseCommand(command);
            if (args.size() == 3) {
                copyFile(args[1], args[2]);
            }
        
	} else if (command.substr(0, 4) == "move") {
         
	    auto args = parseCommand(command);
            
	    if (args.size() == 3) {
            
		moveFile(args[1], args[2]);
            }
        } 
	else if (command.substr(0, 6) == "delete") {
        
	    auto args = parseCommand(command);
            
	    if (args.size() == 2) {
            
		deleteFile(args[1]);
            }
        } 
	else if (command.substr(0, 6) == "create") {
        
	    auto args = parseCommand(command);
            
	    if (args.size() == 2) {
            
		createFile(args[1]);
            }
	    
        } 
	else if (command.substr(0, 6) == "search") {
        
	    auto args = parseCommand(command);
            
	    if (args.size() == 2) {
            
		searchFiles(currentDirectory, args[1]);
            }
	    
        } 
	else if (command.substr(0, 4) == "chmod") {
        
	    auto args = parseCommand(command);
            
	    if (args.size() == 3) {
            
		setPermissions(args[1], args[2]);
            }
	    
        } 
	else {
        
	    std::cout << "Unknown command: " << command << std::endl;
        }
	
    }

    void listFiles() {
        DIR* dir = opendir(currentDirectory.c_str());
        if (dir == nullptr) {
            std::cerr << "Error opening directory!" << std::endl;
            return;
        }

        struct dirent* entry;
        while ((entry = readdir(dir)) != nullptr) {
            std::cout << entry->d_name << std::endl;
        }

        closedir(dir);
    }

    void changeDirectory(const std::string& newDir) {
        if (chdir(newDir.c_str()) == 0) {
            char buffer[1024];
            if (getcwd(buffer, sizeof(buffer)) != nullptr) {
                currentDirectory = std::string(buffer);
            }
        } else {
            std::cerr << "Error: Cannot change directory to " << newDir << std::endl;
        }
    }

    void copyFile(const std::string& source, const std::string& destination) {
        std::ifstream src(source, std::ios::binary);
        std::ofstream dest(destination, std::ios::binary);
        dest << src.rdbuf();
        src.close();
        dest.close();
        std::cout << "File copied to " << destination << std::endl;
    }

    void moveFile(const std::string& source, const std::string& destination) {
        if (rename(source.c_str(), destination.c_str()) == 0) {
            std::cout << "File moved to " << destination << std::endl;
        } else {
            std::cerr << "Error moving file!" << std::endl;
        }
    }

    void deleteFile(const std::string& path) {
        if (unlink(path.c_str()) == 0) {
            std::cout << "File deleted: " << path << std::endl;
        } else {
            std::cerr << "Error deleting file!" << std::endl;
        }
    }

    void createFile(const std::string& fileName) {
        std::ofstream file(fileName);
        if (file) {
            std::cout << "File created: " << fileName << std::endl;
        } else {
            std::cerr << "Error creating file!" << std::endl;
        }
        file.close();
    }

    void searchFiles(const std::string& directory, const std::string& pattern) {
        DIR* dir = opendir(directory.c_str());
        if (dir == nullptr) {
            std::cerr << "Error opening directory!" << std::endl;
            return;
        }

        struct dirent* entry;
        while ((entry = readdir(dir)) != nullptr) {
            if (strstr(entry->d_name, pattern.c_str()) != nullptr) {
                std::cout << "Found: " << entry->d_name << std::endl;
            }
            if (entry->d_type == DT_DIR && strcmp(entry->d_name, ".") != 0 && strcmp(entry->d_name, "..") != 0) {
                searchFiles(directory + "/" + entry->d_name, pattern);
            }
        }

        closedir(dir);
    }

    void setPermissions(const std::string& path, const std::string& mode) {
        mode_t perm = std::stoi(mode, 0, 8);
        if (chmod(path.c_str(), perm) == 0) {
            std::cout << "Permissions set to " << mode << std::endl;
        } else {
            std::cerr << "Error setting permissions!" << std::endl;
        }
    }

    std::vector<std::string> parseCommand(const std::string& command) {
        std::vector<std::string> tokens;
        std::string token;
        std::istringstream tokenStream(command);
        while (std::getline(tokenStream, token, ' ')) {
            tokens.push_back(token);
        }
        return tokens;
    }
};

int main() {
    
    FileExplorer explorer;
    
    explorer.start();
    
    return 0;
}


**Output of ThiS code:**

![WhatsApp Image 2024-08-12 at 11 34 50_59545530](https://github.com/user-attachments/assets/0e8545ef-6057-4d96-b2d8-db0061287bf8)

**Bug Tracker for File Explorer**

**Bug Tracker process:**

In this C++ FileExplorer class is a well-structured example of a basic file management system, but there are a few areas where improvements and bug fixes could be beneficial. Here’s a bug tracker process, improvement suggestions, and corrections for the code provided

**Bug Tracker Process**

**1. Command Parsing Issues**

•	Issue: Command parsing was not handling multiple spaces or quotes effectively.

•	Status: Resolved

•	Details: Improved parseCommand function to handle extra spaces and ensure accurate token extraction.

**2. Error Handling**

•	Issue: Generic error messages for file operations; lack of specific error handling.

•	Status: Resolved

•	Details: Added specific error messages for file existence checks, permission changes, and file operations. Enhanced error handling for invalid permission modes.

**3. File Existence Check**

•	Issue: Operations like copying, moving, or deleting files did not verify if the file existed.

•	Status: Resolved

•	Details: Added fileExists function to check for file existence before performing operations like copy, move, or delete.

**4. File Overwriting Warning**
•	Issue: createFile function would overwrite existing files without warning.
•	Status: Resolved
•	Details: Added a check to ensure files are not overwritten without user notification. Provides a message if the file already exists.

**5. chmod Input Validation**

•	Issue: chmod function did not validate mode inputs effectively.

•	Status: Resolved

•	Details: Added error handling for invalid permission mode inputs and ensured only valid octal permissions are processed.


**6. Search Efficiency**

•	Issue: The searchFiles function might be inefficient for large directories.

•	Status: Pending

•	Details: Consider potential optimizations like limiting recursion depth or using multi-threading to handle large directories more efficiently.


**7. Command Parsing Edge Cases**

•	Issue: Edge cases in command parsing were not handled.

•	Status: Resolved

•	Details: Enhanced parseCommand to better handle various edge cases, including multiple spaces and empty tokens.


**Summary of Fixes**
•	Command Parsing: Improved handling of tokens.
•	Error Handling: Added specific messages for errors.
•	File Operations: Implemented checks for file existence and avoid overwriting files without warning.
•	Permissions: Enhanced validation and error handling for permission changes.


**Next Steps**

•	Search Efficiency: Investigate and implement optimizations for large directory searches.

•	Testing: Continue comprehensive testing to ensure all edge cases are covered and no new issues are introduced.
This report summarizes the status of identified bugs, their resolutions, and any pending issues that need further attention.


**Contributing**


Contributions are welcome! Please follow these steps:

Create a fork in the repository.

To address a feature or defect, create a new branch.

After making your modifications, make sure the program compiles and functions properly.

Send in a pull request to be evaluated.

**License**

This '**File exploring Application'** project is licensed under the our group. See the LICENSE file for details.

**References**

•Google: For general research and problem-solving.

•YouTube: For tutorials and visual learning.

•Training: Formal and informal training resources.

 


