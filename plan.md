Below is a complete implementation plan for adding a motorcycle parts inventory feature to your Next.js project. This plan covers new API endpoints, a shared in‑memory library, and modern UI components (dashboard page, table, search, and form) with proper error handling and best practices.

---

**1. API Endpoints**

- **Create Global Inventory Store (src/lib/inventory.ts):**  
 – Define an in‑memory array (e.g. const inventoryParts = []) to store parts.  
 – Export functions:  
  - getInventoryParts() – returns the array.  
  - addInventoryPart(data) – validates and pushes a new part with an auto‑generated id.  
  - updateInventoryPart(id, data) – finds and updates an existing part, throwing a 404 error if not found.  
  - deleteInventoryPart(id) – removes a part by id with validation.  
 – Ensure try‑catch blocks and input error handling.

- **Create API Route for Collection (src/app/api/inventory/route.ts):**  
 – Implement GET to respond with JSON from getInventoryParts().  
 – Implement POST to validate incoming JSON and call addInventoryPart(), returning the created object.  
 – Use proper HTTP status codes and JSON error messages.

- **Create API Route for Individual Parts (src/app/api/inventory/[id]/route.ts):**  
 – Implement PUT to update a motorcycle part by id and DELETE to remove it.  
 – Include error handling: returning 404 if the part is not found and 500 for unexpected errors.

---

**2. UI Pages & Components**

- **Inventory Dashboard Page (src/app/inventory/page.tsx):**  
 – Create a new Next.js page that fetches inventory parts from the API on mount (using useEffect).  
 – Display a header “Motorcycle Parts Inventory,” a search bar, and a modern-styled container.  
 – Include an “Add New Part” button that opens a modal with InventoryForm.  
 – Maintain state (parts list, loading, error, modal open, and selected part for editing).

- **InventoryTable Component (src/components/inventory/InventoryTable.tsx):**  
 – Render a modern table showing columns (Part Name, SKU, Category, Quantity, Price, Actions).  
 – For each row, include “Edit” and “Delete” buttons that trigger callbacks (provided via props) to open the form modal or call deletion API.  
 – Apply clean typography, spacing, and layout using existing UI components from src/components/ui.

- **InventoryForm Component (src/components/inventory/InventoryForm.tsx):**  
 – Build a modal form with fields: Part Name, SKU, Category (dropdown with options like Engine, Electrical, Body, etc.), Quantity, Price, Description.  
 – Use controlled components with validation messages before submission.  
 – On submit, call the API (POST for new parts, PUT for edits) and return status messages if errors occur.

- **Optional InventorySearch Component (src/components/inventory/InventorySearch.tsx):**  
 – Render a search input with a placeholder “Search parts…” and debounce on change to filter the parts list.  
 – Trigger a callback (passed via props) that filters the InventoryTable.

- **Update components.json:**  
 – Add entries for InventoryTable, InventoryForm, and (if created) InventorySearch with their respective paths.

- **Global Styles (src/app/globals.css):**  
 – Optionally add new CSS rules (e.g. for .inventory-dashboard, .inventory-table) to maintain a consistent modern look with ample whitespace, refined typography, and a clean layout.

- **README.md:**  
 – Add a section documenting the Motorcycle Parts Inventory feature (overview, API endpoints, and instructions for managing parts).

---

**3. Error Handling & Best Practices**

- Use try‑catch in API endpoints and provide HTTP error codes (400 for bad requests, 404 for not found, etc.).  
- Validate form inputs on both client and server.  
- Provide user feedback (using built‑in alert/dialog components from src/components/ui) when errors occur or on successful operations.  
- Ensure API calls are wrapped with loading states and error messages in the dashboard.

---

**Summary**  
- An in‑memory store in src/lib/inventory.ts centralizes CRUD functions for parts.  
- Two API route files (collection and individual) in src/app/api/inventory/ handle GET/POST and PUT/DELETE respectively with proper error handling.  
- A new inventory dashboard page (src/app/inventory/page.tsx) integrates InventoryTable, (optional) InventorySearch, and a modal InventoryForm for adding/editing parts using modern UI design.  
- Components use existing UI elements from src/components/ui, ensuring consistency in typography, spacing, and layout.  
- The README.md is updated to document the new feature and API endpoints.
