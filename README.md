# ApkVision

Fullscreen Android WebView app for [apkvision.org](https://apkvision.org) with an integrated in-app download manager, built in Kotlin.

## Features

*   **Fullscreen WebView**: Provides a clean, immersive browsing experience by utilizing the entire screen.
*   **Integrated Download Manager**: Handles downloads directly within the app, offering progress notifications and saving files to the device's standard Downloads directory.
*   **Intuitive Navigation**: Seamlessly navigate back through web history within the app; exits on reaching the initial page.
*   **Modern Android Development**: Built using Kotlin, following the latest Android development practices, and leveraging Android Gradle Plugin (AGP) 8.4.0.
*   **Optimized Resource Usage**: App icons are consolidated into a single `drawable` resource, reducing APK size while maintaining visual quality.

## Building the APK

This project uses Gradle for building.

### Prerequisites

*   Android SDK
*   Java Development Kit (JDK) 17 or higher
*   Git

### Instructions

1.  **Clone the Repository**:
    ```bash
    git clone https://github.com/Dreamyboyyt/ApkVision.git
    cd ApkVision
    ```

2.  **Build Debug APK**:
    To build a debug version of the application:
    ```bash
    ./gradlew assembleDebug
    ```
    The generated APK will be located at `app/build/outputs/apk/debug/app-debug.apk`.

3.  **Build Release APK**:
    For a signed release APK (requires GitHub Actions secrets, see below):
    ```bash
    ./gradlew assembleRelease
    ```
    The generated APK will be located at `app/build/outputs/apk/release/app-release.apk`.

## GitHub Workflows

This project utilizes GitHub Actions for automated builds and releases.

*   **`build-apk.yml`**:
    *   **Purpose**: Builds an unsigned debug APK for every push to `main` or manual trigger.
    *   **Trigger**: `workflow_dispatch` (manual)
    *   **Output**: An unsigned debug APK artifact.

*   **`build-release.yml`**:
    *   **Purpose**: Builds a *signed* release APK and creates a GitHub Release with an automatically incremented version tag (e.g., `v1.1`, `v1.2`).
    *   **Trigger**: `workflow_dispatch` (manual)
    *   **Requirements**: Requires specific [GitHub Secrets](#github-secrets) to be configured for APK signing.
    *   **Output**: A signed release APK uploaded as a GitHub Release asset.

*   **`zip-project.yml`**:
    *   **Purpose**: Zips the entire project directory and uploads it as an artifact.
    *   **Trigger**: `workflow_dispatch` (manual)
    *   **Output**: A `project.zip` artifact.

### GitHub Secrets

For the `build-release.yml` workflow to function correctly (especially for APK signing), you must configure the following secrets in your GitHub repository settings (`Settings > Secrets and variables > Actions`):

*   `SIGNING_KEY_BASE64`: Your base64-encoded release keystore file.
    (Generate with: `base64 -w 0 your-release-key.keystore`)
*   `KEYSTORE_PASSWORD`: The password for your keystore.
*   `KEY_ALIAS`: The alias for your key within the keystore.
*   `KEY_PASSWORD`: The password for your key.

## Contributing

Contributions are welcome! Please feel free to open issues or submit pull requests.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
