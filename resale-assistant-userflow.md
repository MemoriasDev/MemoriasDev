# Piff Resale Assistant - User Flow Documentation

## Overview

The Piff platform serves multiple distinct user types, each with their own workflows and interactions. This document outlines all user journeys within the application, from initial setup to daily operations.

## User Types & Roles

### 1. Super Admin
- **Scope**: Platform-wide administration
- **Access**: All stores and system-level functions
- **Authentication**: Email/password with super admin flag

### 2. Store Owner
- **Scope**: Complete control over their store
- **Access**: All features within their store
- **Authentication**: Email/password linked to store

### 3. Store Employee
- **Scope**: Permission-based access within store
- **Access**: Based on assigned permissions
- **Authentication**: Email/password with role restrictions

### 4. Seller
- **Scope**: Submit items and track submissions
- **Access**: Quote system and personal item tracking
- **Authentication**: Phone number verification

## User Journey Flows

## Super Admin Flows

### Super Admin Login & Store Management
**Entry Point**: `/admin` or direct URL access

1. **Authentication**
   - Navigate to super admin sign-in page
   - Enter email and password
   - System validates super admin flag
   - Redirect to super admin dashboard

2. **Store Creation**
   - Click "Create New Store" 
   - Enter store details:
     - Owner email address
     - Shopify API credentials (API key, secret, domain)
   - System validates Shopify connection
   - Creates store record and owner link code
   - Sends owner invitation email

3. **Store Management**
   - View all stores in system
   - Toggle store active/inactive status
   - Access individual store settings
   - Configure platform-level store settings:
     - Import charges for new/existing products
     - System-wide configurations

4. **Store Maintenance**
   - Refresh webhook subscriptions
   - Debug store integration issues
   - Delete stores (dev environment only)

**Key Files**:
- Frontend: `/react/src/components/pages/superAdmin/`
- Backend: `/api/src/resolvers/superAdmin.ts`

---

## Store Owner Flows

### Initial Store Setup
**Entry Point**: Email invitation from super admin

1. **Account Creation**
   - Click link in invitation email
   - Verify email matches invitation
   - Create password
   - Account automatically linked to store

2. **Store Configuration**
   - **Basic Information Setup**:
     - Store display name and description
     - Upload light and dark logos
     - Set headquarters address
     - Configure policy URLs (TOS, Privacy, FAQ)

   - **Quote Settings Configuration**:
     - Set accepted payout types (cash, store credit, consignment)
     - Configure accepted brands (all brands or specific list)
     - Allow/disallow new product submissions
     - Set employee commission percentage
     - Configure packing instructions

   - **Shipping Defaults**:
     - Set who pays for shipping to store (seller/store)
     - Set who pays for return shipping
     - Configure shipping deduction from payout

   - **Product Conditions**:
     - Create custom product condition categories
     - Set payout likelihood rules for each condition
     - Configure condition-specific settings

3. **Employee Management**
   - Send employee invitations by email
   - Configure employee permissions:
     - Edit quote settings
     - Edit authentication settings
     - Edit inventory settings
     - Create items
     - Edit commission settings
     - Edit StockX settings
   - Set employee alert preferences

4. **Financial Setup**
   - Configure Checkbook.io integration:
     - Business information
     - Bank account details
     - Verification process
   - Set automatic payout processing timeframe

**Key Files**:
- Frontend: `/react/src/components/pages/store/CreateOwnerAccountPage/`
- Backend: `/api/src/resolvers/siteUser.ts` (registerOwner)

### Daily Store Operations

1. **Quote Management**
   - **Review Submitted Quotes**:
     - View quote list with filters (status, date, submitter)
     - Access individual quote details
     - Review line items and seller information
     - Accept/reject individual items or entire quotes

   - **Quote Communication**:
     - Send messages to sellers
     - View message history
     - Handle seller responses and negotiations

2. **Authentication Workflow Management**
   - **Configure Authentication Process**:
     - Set required images by product type
     - Create custom authentication questions
     - Define rejection reasons
     - Configure email notifications

   - **Process Authentication Requests**:
     - Review submitted items awaiting authentication
     - Follow step-by-step authentication workflow
     - Make authentication decisions
     - Handle rejections with detailed feedback

3. **Inventory Management**
   - **Product Catalog**:
     - Search and filter products
     - View product details and variants
     - Manage product information and pricing
     - Create custom products

   - **Inventory Monitoring**:
     - Set up inventory alerts by brand/product type
     - Monitor stock levels across locations
     - Handle low inventory notifications

4. **Sales & Order Management**
   - **Order Processing**:
     - View sales ledger with order details
     - Mark commission as paid
     - Track order fulfillment

   - **StockX Integration**:
     - View StockX market data
     - List items on StockX marketplace
     - Manage StockX portfolio

5. **Financial Management**
   - **Payout Processing**:
     - Configure automatic payout schedules
     - Manual payout processing
     - Track payout history

   - **Commission Tracking**:
     - View employee commission reports
     - Mark commissions as paid

**Key Files**:
- Frontend: `/react/src/components/pages/store/`
- Backend: Multiple resolvers for different functionalities

---

## Store Employee Flows

### Employee Onboarding
**Entry Point**: Email invitation from store owner

1. **Accept Invitation**
   - Click invitation link
   - Create account with email/password
   - Account automatically linked to store with assigned permissions

2. **Permission-Based Access**
   - Dashboard shows only permitted functions
   - Navigation reflects available permissions
   - Attempt to access restricted features shows error

### Daily Employee Operations

Employee workflows depend on assigned permissions:

1. **Quote Processing** (if permitted):
   - Same as store owner quote management
   - May have restrictions on certain actions

2. **Authentication Processing** (if permitted):
   - Follow authentication workflow
   - Process items through authentication steps
   - Make authentication decisions

3. **Inventory Management** (if permitted):
   - Update product information
   - Create new inventory items
   - Manage product variants

4. **Customer Communication**:
   - Respond to seller messages
   - Handle customer inquiries
   - Update sellers on item status

**Key Files**:
- Frontend: Same as store owner but with permission-based UI
- Backend: Permission checks in resolvers

---

## Seller Flows

### Seller Registration & Onboarding
**Entry Point**: Store-specific URL (e.g., `/{store-domain}/sellers`)

1. **Phone Number Registration**
   - Enter phone number
   - Accept terms of service
   - Receive SMS verification code
   - Enter verification code
   - Account created and authenticated

2. **Profile Setup** (Optional):
   - Add full name
   - Add email address
   - Add mailing address
   - Upload profile picture

### Quote Creation Process

1. **Start New Quote**
   - Navigate to quote builder
   - System creates draft quote automatically

2. **Add Items to Quote**
   - **Search for Existing Products**:
     - Search store's product catalog
     - Search StockX for market data
     - Select matching product

   - **Create New Product**:
     - Enter product details (brand, title, type)
     - Specify gender and category

3. **Item Details Entry**:
   - Select product condition from store's options
   - Enter size
   - Set asking price
   - Choose payout type (cash, store credit, consignment)
   - Add notes/description
   - Upload product images (multiple images supported)
   - Optionally enter SKU

4. **Quote Review & Submission**:
   - Review all line items
   - See payout likelihood estimates
   - Make final adjustments
   - Submit quote to store

### Post-Submission Tracking

1. **Quote Status Monitoring**:
   - View submitted quotes list
   - Check quote status (submitted, rejected, accepted, etc.)
   - Receive notifications for status changes

2. **Item-Level Tracking**:
   - View individual line item status
   - Track item through entire lifecycle:
     - Shipping preparation
     - In transit to store
     - Authentication process
     - Listing and sale
     - Payment processing

3. **Communication**:
   - Receive messages from store staff
   - Respond to store inquiries
   - View message history

4. **Shipping Coordination**:
   - Receive shipping labels (if store provides)
   - Coordinate item pickup/dropoff
   - Track shipment status

### Consignment Item Management

1. **Active Consignment Tracking**:
   - View items currently on consignment
   - Check listing status and pricing
   - Monitor sales performance
   - Review market feedback

2. **Consignment Responses**:
   - Respond to store pricing proposals
   - Make decisions on discount requests
   - Handle return requests for unsold items

**Key Files**:
- Frontend: `/react/src/components/pages/sellersPortal/`
- Backend: `/api/src/resolvers/quote.ts`, `/api/src/resolvers/siteUser.ts`

---

## Detailed Workflow Processes

### Authentication Workflow (Store Staff)

**Entry Point**: Item status becomes "awaitingAuthentication"

1. **Start Authentication**:
   - Navigate to authentication queue
   - Select item for authentication
   - Click "Start Authentication"
   - System creates authentication record

2. **Confirm Contents** (Step 1):
   - Verify received item matches submission
   - Check physical condition against photos
   - Mark step complete or reject with reason

3. **Intake Pictures** (Step 2):
   - Take required photos based on product type
   - Upload photos to system
   - System validates all required images present
   - Mark step complete

4. **Validate Details** (Step 3):
   - Verify product information accuracy
   - Check brand, model, size, etc.
   - Update details if necessary
   - Mark step complete

5. **Validate Condition** (Step 4):
   - Assess actual item condition
   - Select condition from store's categories
   - Add condition notes
   - Mark step complete

6. **Validate Authenticity** (Step 5):
   - Perform authenticity checks
   - Answer product-specific authentication questions
   - Mark step complete with authenticator identification

7. **Complete Authentication**:
   - **If Approved**:
     - Set listing details (price, location)
     - Configure StockX listing (if applicable)
     - Process payout according to item terms
     - List item for sale
   
   - **If Rejected**:
     - Select rejection reason
     - Add detailed comments
     - Upload supporting photos
     - Configure return shipping
     - Send rejection notification

**Key Files**:
- Frontend: `/react/src/components/pages/store/authentication/AuthenticationWorkflowPage/`
- Backend: `/api/src/resolvers/authentication.ts`

### Bulk Import Process (Store Staff)

**Entry Point**: Store navigation → Bulk Import

1. **Create Import Session**:
   - Click "Create New Import"
   - System creates draft import record

2. **Add Sellers**:
   - Search existing sellers by phone/name
   - Register new sellers if not found
   - Add sellers to import session

3. **Add Line Items**:
   - For each seller, add their items:
     - Search/select products
     - Set item details (condition, size, pricing)
     - Set seller and listing prices
     - Configure consignment rates
     - Upload item photos

4. **Review & Submit**:
   - Review all items and sellers
   - Verify pricing and settings
   - Submit import for processing
   - Monitor import progress via real-time updates

5. **Post-Import Processing**:
   - Items automatically flow into authentication queue
   - Sellers receive notifications about their items
   - Store staff process items through normal workflow

**Key Files**:
- Frontend: `/react/src/components/pages/store/bulkImport/`
- Backend: `/api/src/resolvers/import.ts`

---

## Navigation & User Experience Patterns

### Responsive Design Patterns
- Mobile-first design for sellers (primary mobile users)
- Desktop-optimized for store staff (professional use)
- Progressive web app capabilities

### Common UI Patterns

1. **Search & Filter**:
   - Product search with multiple criteria
   - Quote/item filtering by status, date, seller
   - Real-time search suggestions

2. **Status Indicators**:
   - Color-coded status badges
   - Progress indicators for multi-step processes
   - Real-time status updates

3. **Data Tables**:
   - Sortable columns
   - Pagination controls
   - Bulk action capabilities
   - Export functionality

4. **Modal Workflows**:
   - Multi-step forms in modals
   - Confirmation dialogs for critical actions
   - Image lightbox for product photos

### Notification Systems

1. **In-App Notifications**:
   - Real-time notifications for status changes
   - Notification history and read status
   - Role-based notification preferences

2. **Email Notifications**:
   - Quote status changes
   - Authentication results
   - System alerts and updates

3. **SMS Notifications** (via Firebase):
   - Account verification
   - Critical status updates

---

## Error Handling & Edge Cases

### Authentication Failures
- Invalid credentials → Clear error messages
- Expired sessions → Automatic redirect to login
- Permission denials → Helpful explanation of required permissions

### Data Validation Errors
- Form validation with field-level error messages
- File upload restrictions and error handling
- Required field validation

### Network & Integration Failures
- Shopify API failures → Graceful degradation
- StockX integration issues → Alternative workflows
- Shipping API problems → Manual fallback options

### Business Logic Edge Cases
- Duplicate submissions → Detection and prevention
- Pricing conflicts → Clear resolution workflows
- Inventory synchronization issues → Error reporting and resolution

---

## Performance Considerations

### Data Loading Patterns
- GraphQL query optimization
- Pagination for large datasets
- Image lazy loading
- Progressive data loading

### Caching Strategies
- Apollo Client caching
- Static asset caching
- API response caching where appropriate

### Mobile Performance
- Optimized image delivery
- Minimal initial bundle size
- Offline capability for core features

---

## Accessibility & Usability

### Accessibility Features
- Keyboard navigation support
- Screen reader compatibility
- High contrast mode support
- Alt text for images

### Usability Features
- Clear navigation hierarchy
- Contextual help and tooltips
- Undo functionality for critical actions
- Bulk operations for efficiency

---

## Integration Touchpoints

### External System Interactions

1. **Shopify Integration**:
   - Real-time product synchronization
   - Order webhook processing
   - Inventory level updates
   - Multi-location support

2. **StockX Integration**:
   - Product search and matching
   - Market data retrieval
   - Automated listing creation
   - Portfolio management

3. **Payment Processing**:
   - Checkbook.io payout processing
   - Bank account verification
   - Payment status tracking

4. **Shipping Services**:
   - ShipEngine label generation
   - Rate shopping across carriers
   - Tracking integration

5. **Communication Services**:
   - SendGrid email delivery
   - Firebase SMS authentication
   - Push notification support

---

## Security & Privacy Considerations

### User Data Protection
- Secure authentication flows
- Personal information encryption
- Payment data isolation
- Image storage security

### Business Data Security
- Multi-tenant data isolation
- Role-based access controls
- Audit logging for sensitive actions
- Secure API communications

### Compliance Considerations
- Terms of service acceptance tracking
- Privacy policy compliance
- Data retention policies
- User consent management

---

This comprehensive user flow documentation demonstrates the sophisticated multi-user system that Piff Legacy provided, with distinct workflows tailored to each user type's needs while maintaining seamless integration between all parts of the consignment business process.
