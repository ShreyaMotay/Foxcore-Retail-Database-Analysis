# # Foxcore Retail Database Implementation

## Table of Contents
- [Introduction](#introduction)
- [Problem Statement](#problem-statement)
- [Database Entities and Relationships](#database-entities-and-relationships)
- [Database Schema](#database-schema)
- [Data Population](#data-population)
- [Report Queries](#report-queries)
- [Conclusion](#conclusion)
- [Future Enhancements](#future-enhancements)
- [Contact Information](#contact-information)

## Introduction
Foxcore Retail, founded by Liam Corrigan and Mitchell Fox, started as a small business selling novelty items at events across Ontario. Over time, the business expanded, and the need for a more structured and efficient system for sales tracking and data management became apparent. This project aims to address the inefficiencies through the implementation of a relational database solution to centralize data and enhance reporting capabilities.

## Problem Statement
The primary challenges faced by Foxcore Retail included:
- Manual sales tracking and paper-based record-keeping.
- Fragmented and disjointed data management.
- Errors in tracking sales, inventory, and overall performance.
- Lack of centralized data, leading to missed opportunities for insights and optimization.

## Database Entities and Relationships
The relational database is structured to represent the following key entities:
- **Event**: Represents an occurrence at a venue.
- **Venue**: The location where the event takes place.
- **Booth**: A specific spot at the event where sales are made.
- **Product**: Items sold by the company.
- **Salesperson**: Staff managing the booths and sales.
- **Sales**: Transactions involving products sold by salespeople.

### Relationships:
- Each event occurs at a venue.
- Each event has one or more booths.
- Each booth is managed by one or more salespeople.
- Sales transactions are tied to products and salespeople.

## Database Schema
The following tables represent the core database structure:
- **Event**: EventID, EventName, StartDate, EndDate, EventType.
- **Venue**: VenueID, VenueName, Address.
- **Booth**: BoothID, EventID, Location.
- **Product**: ProductID, ProductName, WholesaleCost, MinSellingPrice.
- **Salesperson**: SalespersonID, FirstName, LastName.
- **Sales**: SaleID, BoothID, SalespersonID, ProductID, QuantitySold, SellingPrice.

## Data Population
For demonstration purposes, data was populated into the database including sample records for events, venues, booths, products, salespeople, and sales transactions.

### Example Data:
- **Events**: Music Festival, Trade Show, Rib Fest.
- **Products**: Bubble Gun, Cooling Towel, Emoji Pillow.
- **Salespeople**: John Doe, Jane Smith, Michael Johnson.
- **Sales**: Transactions were recorded for each event and product.

## Report Queries
Two key reports were generated from the database to analyze sales performance:

1. **Total Sales by Event Type**:
   ```sql
   SELECT e.EventType, SUM(s.QuantitySold) AS TotalSales
   FROM Event e
   LEFT JOIN Booth b ON e.EventID = b.EventID
   LEFT JOIN Sales s ON b.BoothID = s.BoothID
   GROUP BY e.EventType;
