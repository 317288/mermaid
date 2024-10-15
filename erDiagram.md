```mermaid
erDiagram
    USER {
        INT UserID PK
        VARCHAR Username
        VARCHAR Email
        VARCHAR Password
        VARCHAR FullName
        ENUM Role
        VARCHAR PhoneNumber
        TEXT Address
        ENUM AccountStatus
        DATETIME RegisteredDate
        DATETIME LastLogin
    }

    ITEM {
        INT ItemID PK
        VARCHAR Name
        TEXT Description
        VARCHAR Category
        ENUM Condition
        DECIMAL AskingPrice
        DECIMAL ReservePrice
        DATETIME StartDate
        DATETIME EndDate
        INT SellerID FK
        VARCHAR ImageURL
        VARCHAR Location
    }

    AUCTION {
        INT AuctionID PK
        INT ItemID FK
        DATETIME StartTime
        DATETIME EndTime
        DECIMAL CurrentHighestBid
        ENUM AuctionStatus
        INT SellerID FK
        DECIMAL BidIncrement
        INT WinnerID FK
    }

    BID {
        INT BidID PK
        INT AuctionID FK
        INT BuyerID FK
        DECIMAL BidAmount
        DATETIME BidTime
        ENUM BidStatus
    }

    TRANSACTION {
        INT TransactionID PK
        INT AuctionID FK
        INT BuyerID FK
        DECIMAL FinalAmount
        ENUM Currency
        DATETIME TransactionStartDate
        DATETIME TransactionEndDate
        ENUM PaymentMethod
        ENUM PaymentStatus
        TEXT ShippingAddress
    }

    WATCHLIST {
        INT WatchlistID PK
        INT BuyerID FK
        INT AuctionID FK
        ENUM NotificationStatus
    }

    RATING {
        INT RatingID PK
        INT UserID FK
        INT RatedByUserID FK
        INT RatingScore
        TEXT Comment
    }

    DISPUTE {
        INT DisputeID PK
        INT TransactionID FK
        INT DisputeByUserID FK
        ENUM DisputeStatus
        TEXT Content
        TEXT Resolution
        DATETIME RaisedDate
        DATETIME ResolvedDate
    }

    NOTIFICATION {
        INT NotificationID PK
        INT UserID FK
        ENUM NotificationType
        TEXT Message
        ENUM NotificationStatus
        DATETIME CreatedDate
    }

    USER ||--o{ ITEM : "sells"
    USER ||--o{ AUCTION : "creates"
    USER ||--o{ BID : "places"
    USER ||--o{ WATCHLIST : "watches"
    USER ||--o{ RATING : "is rated by"
    USER ||--o{ TRANSACTION : "participates in"
    ITEM ||--o{ AUCTION : "is auctioned in"
    AUCTION ||--o{ BID : "receives"
    AUCTION ||--o{ TRANSACTION : "is finalized in"
    AUCTION ||--o{ WATCHLIST : "is added to"
    TRANSACTION ||--o{ DISPUTE : "is involved in"
    USER ||--o{ NOTIFICATION : "receives"

