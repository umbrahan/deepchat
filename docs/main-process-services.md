# Main Process Services

This document outlines the services provided by the Electron main process in this application. These services are primarily implemented as presenters and manage various aspects of the application's functionality.

1.  **`WindowPresenter`**:
    *   Manages the lifecycle of application windows (creation, destruction, showing, hiding).
    *   Handles window-related events and interactions.
    *   Sends events and data to renderer processes.

2.  **`SQLitePresenter`**:
    *   Manages the connection to the SQLite database.
    *   Provides an interface for other services to interact with the database (CRUD operations).
    *   Likely used for storing chat history, user preferences, application state, etc.

3.  **`LLMProviderPresenter`**:
    *   Manages configurations for various Large Language Model (LLM) providers (e.g., OpenAI, local models).
    *   Allows users to select and switch between different LLM providers.
    *   Handles API interactions with the configured LLM providers.
    *   Manages custom models for each provider.

4.  **`ConfigPresenter`**:
    *   Manages overall application configuration and settings.
    *   Handles loading and saving of settings (e.g., proxy settings, logging preferences, provider API keys, UI themes).
    *   Provides access to configuration values for other services.

5.  **`ThreadPresenter`**:
    *   Manages chat threads and conversations.
    *   Interacts with `SQLitePresenter` to store and retrieve conversation data.
    *   Orchestrates communication between the user interface, `LLMProviderPresenter`, and the database for chat functionalities.
    *   Handles message creation, editing, and context management.

6.  **`DevicePresenter`**:
    *   Handles device-specific information or functionalities.
    *   (Purpose might need further clarification based on its specific implementation details, but generally relates to interacting with the user's device hardware or system features).

7.  **`UpgradePresenter`**:
    *   Manages application updates and upgrades.
    *   Checks for new versions.
    *   Handles the download and installation of updates.
    *   Notifies users about update status.

8.  **`ShortcutPresenter`**:
    *   Manages global keyboard shortcuts for the application.
    *   Allows users to perform actions quickly using keyboard commands (e.g., open settings, new chat).

9.  **`FilePresenter`**:
    *   Handles various file-related operations.
    *   Likely supports different file types (text, images, code, documents) for use as context in chats or other features.
    *   May include functionalities like file parsing, preview generation, or managing file attachments.

10. **`McpPresenter`**:
    *   Manages aspects of the "My Copilot Platform" (MCP).
    *   Handles MCP server management (starting, stopping).
    *   Manages MCP client interactions and tool integrations.
    *   Facilitates communication with Python runner for MCP tools.

11. **`SyncPresenter`**:
    *   Handles data synchronization features.
    *   Likely responsible for backing up application data (e.g., to a cloud service or local file).
    *   May also handle importing data from backups or other sources.

12. **`DeeplinkPresenter`**:
    *   Manages deep linking functionalities.
    *   Allows the application to be launched or navigated to specific views or actions via custom URL schemes (e.g., `deepchat://...`).
    *   Handles parsing of deep links and routing to the appropriate application state.

13. **`NotificationPresenter`**:
    *   Manages system notifications for the application.
    *   Displays notifications to the user for events like new messages, errors, or updates.
    *   Handles user interactions with notifications.

14. **`TabPresenter`**:
    *   Manages tabs within the application windows, similar to browser tabs.
    *   Allows users to have multiple chats or views open simultaneously.
    *   Handles tab creation, switching, and closing.

15. **`TrayPresenter`**:
    *   Manages the application's icon and menu in the system tray (or menu bar on macOS).
    *   Provides quick access to application functionalities like opening the window, quitting, or status indicators.
    *   Handles tray icon events.

## Protocol Handlers (Initialized in `src/main/index.ts`)

Beyond the presenters, the main process also initializes custom protocol handlers:

*   **`deepcdn://`**: Serves static assets (JS, CSS) from the application's resources directory. This is likely used to efficiently load local web content for UI components.
*   **`imgcache://`**: Serves cached images from the user's data directory. This helps in optimizing image loading and reducing redundant downloads.
