# Hito Firmware Architecture

## Overview

Hito uses a system-on-chip (SoC) with an embedded secure element to protect cryptographic operations at the hardware level. The firmware design follows a modular structure, ensuring each component handles a distinct portion of the workflow.

## Core Libraries

1. **libcrypt0 (Basic Crypto Primitives)**
   - Implements fundamental cryptographic functions (e.g., ECDSA, hashing).
   - Ensures low-level operations occur within the secure element.
   - Offers an abstract interface for reliability and data integrity.

2. **libcrypt0_xlm**
   - Specializes in Stellar-specific transaction parsing and signing.
   - Works closely with `libcrypt0` to securely handle transaction creation.
   - Maintains compatibility with Stellar Ledger formats.

3. **libcrypt0_soroban**
   - Extends the crypto primitives for Soroban smart contract operations.
   - Provides secure signing and state verification for Soroban-based dApps.
   - Scales to handle potential future smart contract features on Stellar.

4. **libcrypt0_stellar_ui (UI Elements)**
   - Manages on-device displays and user interactions.
   - Offers intuitive confirmation flows for XLM and Soroban transactions.
   - Ensures clarity in transaction details for end-users.

## Data Flow

1. **Transaction/Contract Data:** Received through the SoC interface.  
2. **Secure Processing:** `libcrypt0` handles cryptographic functions in the secure element.  
3. **Ledger/Contract Logic:** `libcrypt0_xlm` or `libcrypt0_soroban` parse and sign data.  
4. **User Confirmation:** `libcrypt0_stellar_ui` displays details for physical approval.  
5. **Final Signing & Broadcast:** Signed transactions are returned for network submission.
