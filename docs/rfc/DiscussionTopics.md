# Community Discussion Topics

We want to hear from you! Please open a GitHub Issue to discuss any of the following topics. 

### Topic 1: Developer Experience (CLI vs. VSIX)
*   Do you prefer running commands in the terminal (e.g., `pass scaffold Customer --theme dark`), or do you prefer a Visual Studio right-click menu (VSIX) with a GUI?
*   Would you use a CI/CD pipeline command like `pass sync-all` to automatically update code during a build?

### Topic 2: The `pass.json` File
*   Should `pass.json` be checked into source control (git) to ensure team consistency? 
*   Are there other project-level settings we are missing? (e.g., CSS preprocessors like SASS, or specific JS frameworks like React/Vue for MVC).

### Topic 3: Roslyn Merging Limitations
*   Have you experienced scenarios where your C# entities have complex custom attributes or constructors that might break AST merging?
*   How should PASS handle generated code that has been manually deleted by a developer? (Should it re-generate it, or assume the developer deleted it on purpose?)

### Topic 4: Academic Validation
*   If we write a research paper on this, what metrics would convince *you* that this tool is better than the default scaffolder? 
*   (Current proposed metrics: Time saved, Lines of custom code preserved, Maintainability Index).
