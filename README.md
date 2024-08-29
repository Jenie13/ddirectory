#include <iostream>
#include <fstream>
#include <filesystem>
#include <string>

namespace fs = std::filesystem;

void listFiles() {
    for (const auto& entry : fs::directory_iterator(fs::current_path())) {
        std::cout << entry.path().filename().string() << std::endl;
    }
}

void createDirectory() {
    std::string dirName;
    std::cout << "Enter directory name: ";
    std::cin >> dirName;

    if (fs::create_directory(dirName)) {
        std::cout << "Directory created successfully." << std::endl;
    } else {
        std::cout << "Failed to create directory." << std::endl;
    }
}

void changeDirectory() {
    std::string dirPath;
    std::cout << "Enter directory path: ";
    std::cin >> dirPath;

    try {
        fs::current_path(dirPath);
        std::cout << "Directory changed successfully." << std::endl;
    } catch (const fs::filesystem_error& e) {
        std::cout << "Failed to change directory: " << e.what() << std::endl;
    }
}

void removeDirectory() {
    std::string dirName;
    std::cout << "Enter directory name: ";
    std::cin >> dirName;

    std::uintmax_t removedCount = fs::remove_all(dirName);
    if (removedCount > 0) {
        std::cout << "Directory removed successfully." << std::endl;
    } else {
        std::cout << "Failed to remove directory." << std::endl;
    }
}

void removeFile() {
    std::string fileName;
    std::cout << "Enter file name: ";
    std::cin >> fileName;

    if (fs::remove(fileName)) {
        std::cout << "File removed successfully." << std::endl;
    } else {
        std::cout << "Failed to remove file." << std::endl;
    }
}

void copyFile() {
    std::string source, destination;
    std::cout << "Enter source file name: ";
    std::cin >> source;
    std::cout << "Enter destination file name: ";
    std::cin >> destination;

    try {
        fs::copy_file(source, destination, fs::copy_options::overwrite_existing);
        std::cout << "File copied successfully." << std::endl;
    } catch (const fs::filesystem_error& e) {
        std::cout << "Failed to copy file: " << e.what() << std::endl;
    }
}

void moveFile() {
    std::string source, destination;
    std::cout << "Enter source file name: ";
    std::cin >> source;
    std::cout << "Enter destination file name: ";
    std::cin >> destination;

    try {
        fs::rename(source, destination);
        std::cout << "File moved successfully." << std::endl;
    } catch (const fs::filesystem_error& e) {
        std::cout << "Failed to move file: " << e.what() << std::endl;
    }
}

int main() {
    int choice;
    while (true) {
        std::cout << "Directory Management System" << std::endl;
        std::cout << "1. List files" << std::endl;
        std::cout << "2. Create directory" << std::endl;
        std::cout << "3. Change directory" << std::endl;
        std::cout << "4. Remove directory" << std::endl;
        std::cout << "5. Remove file" << std::endl;
        std::cout << "6. Copy file" << std::endl;
        std::cout << "7. Move file" << std::endl;
        std::cout << "8. Exit" << std::endl;
        std::cout << "Enter your choice: ";
        std::cin >> choice;

        switch (choice) {
            case 1:
                listFiles();
                break;
            case 2:
                createDirectory();
                break;
            case 3:
                changeDirectory();
                break;
            case 4:
                removeDirectory();
                break;
            case 5:
                removeFile();
                break;
            case 6:
                copyFile();
                break;
            case 7:
                moveFile();
                break;
            case 8:
                return 0;
            default:
                std::cout << "Invalid choice. Please try again." << std::endl;
        }
    }

    return 0;
}
