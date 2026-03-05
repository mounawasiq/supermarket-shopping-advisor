-- =============================================
-- SUPERMARKET SHOPPING ADVISOR - DATABASE SCHEMA
-- =============================================

-- 1. USERS
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    username VARCHAR(100),
    email VARCHAR(255),
    password VARCHAR(255),
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW()
);

-- 2. SUPERMARKETS (reference table)
CREATE TABLE supermarkets (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) UNIQUE,
    website VARCHAR(255),
    logo_url VARCHAR(255),
    created_at TIMESTAMP DEFAULT NOW()
);

-- 3. PRODUCTS (reference table)
CREATE TABLE products (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255),
    category VARCHAR(100),
    brand VARCHAR(100),
    unit VARCHAR(50),
    created_at TIMESTAMP DEFAULT NOW()
);

-- 4. PRICES
CREATE TABLE prices (
    id SERIAL PRIMARY KEY,
    supermarket_id INT REFERENCES supermarkets(id),
    product_id INT REFERENCES products(id),
    price DECIMAL(10, 2),
    normal_price DECIMAL(10, 2),
    is_on_sale BOOLEAN DEFAULT FALSE,
    sale_description VARCHAR(500),
    date DATE,
    created_at TIMESTAMP DEFAULT NOW()
);

-- 5. BUDGETS
CREATE TABLE budgets (
    id SERIAL PRIMARY KEY,
    user_id INT REFERENCES users(id),
    amount DECIMAL(10, 2),
    frequency VARCHAR(20),
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW()
);

-- 6. SHOPPING LIST
CREATE TABLE shopping_list_items (
    id SERIAL PRIMARY KEY,
    user_id INT REFERENCES users(id),
    product_id INT REFERENCES products(id),
    quantity INT DEFAULT 1,
    added_at TIMESTAMP DEFAULT NOW()
);

-- 7. SPENDING
CREATE TABLE spending (
    id SERIAL PRIMARY KEY,
    user_id INT REFERENCES users(id),
    supermarket_id INT REFERENCES supermarkets(id),
    amount DECIMAL(10, 2),
    date DATE,
    notes VARCHAR(500),
    created_at TIMESTAMP DEFAULT NOW()
);

-- 8. PREDICTIONS
CREATE TABLE predictions (
    id SERIAL PRIMARY KEY,
    user_id INT REFERENCES users(id),
    prediction_type VARCHAR(100),
    prediction_data JSON,
    created_at TIMESTAMP DEFAULT NOW()
);

-- =============================================
-- MIGRATION MODULE (CORE FEATURE)
-- =============================================

-- 9. MIGRATION SETUP COSTS (reference data)
CREATE TABLE migration_setup_costs (
    id SERIAL PRIMARY KEY,
    cost_name VARCHAR(255),
    category VARCHAR(100),
    estimated_cost DECIMAL(10, 2),
    description TEXT,
    cheapest_retailer VARCHAR(100),
    cheapest_price DECIMAL(10, 2),
    estimated_savings DECIMAL(10, 2),
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW()
);

-- 10. USER MIGRATION PROFILE
CREATE TABLE user_migration_profile (
    id SERIAL PRIMARY KEY,
    user_id INT REFERENCES users(id),
    is_immigrant BOOLEAN DEFAULT FALSE,
    arrived_month INT,
    arrived_year INT,
    family_size INT,
    has_children BOOLEAN DEFAULT FALSE,
    setup_budget DECIMAL(10, 2),
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW()
);

-- 11. MIGRATION TRACKING
CREATE TABLE migration_tracking (
    id SERIAL PRIMARY KEY,
    user_id INT REFERENCES users(id),
    cost_item VARCHAR(255),
    planned_amount DECIMAL(10, 2),
    actual_amount DECIMAL(10, 2),
    retailer VARCHAR(100),
    purchased BOOLEAN DEFAULT FALSE,
    purchase_date DATE,
    created_at TIMESTAMP DEFAULT NOW()
);

-- =============================================
-- SEED DATA - SUPERMARKETS
-- =============================================

INSERT INTO supermarkets (name, website) VALUES
('Tesco',       'https://www.tesco.com'),
('Asda',        'https://www.asda.com'),
('Lidl',        'https://www.lidl.co.uk'),
('Sainsburys',  'https://www.sainsburys.co.uk'),
('Morrisons',   'https://www.morrisons.com'),
('Waitrose',    'https://www.waitrose.com'),
('Coop',        'https://www.coop.co.uk');

-- =============================================
-- SEED DATA - MIGRATION SETUP COSTS
-- =============================================

INSERT INTO migration_setup_costs
(cost_name, category, estimated_cost, description, cheapest_retailer, cheapest_price, estimated_savings)
VALUES
('Winter coat (adult)',     'winter',    60.00, 'Warm winter coat for UK weather',    'Primark', 35.00, 25.00),
('Winter coat (child)',     'winter',    45.00, 'Kids warm winter coat',              'Asda',    30.00, 15.00),
('Boots (adult)',           'winter',    50.00, 'Waterproof winter boots',            'Primark', 25.00, 25.00),
('Boots (child)',           'winter',    35.00, 'Kids waterproof boots',              'Asda',    20.00, 15.00),
('Gloves + scarf + hat',    'winter',    20.00, 'Winter accessories bundle',          'Primark', 10.00, 10.00),
('School uniform set',      'school',   120.00, 'Full school uniform per child',      'Asda',    80.00, 40.00),
('School shoes',            'school',    40.00, 'Black school shoes per child',       'Asda',    25.00, 15.00),
('School bag',              'school',    25.00, 'Backpack for school',                'Primark', 15.00, 10.00),
('Stationery pack',         'school',    15.00, 'Pens, pencils, ruler etc',           'Tesco',    8.00,  7.00),
('Bedding set (double)',    'home',      80.00, 'Duvet, pillows, covers',             'Dunelm',  50.00, 30.00),
('Bedding set (single)',    'home',      55.00, 'Single duvet, pillows, covers',      'Dunelm',  35.00, 20.00),
('Towels (set of 4)',       'home',      30.00, 'Bath and hand towels',               'Primark', 18.00, 12.00),
('Curtains/blinds',        'home',      60.00, 'Window coverings for one room',      'Dunelm',  40.00, 20.00),
('Cleaning supplies',       'household', 50.00, 'Bleach, mop, hoover bags etc',      'Lidl',    30.00, 20.00),
('Toiletries starter pack', 'household', 40.00, 'Shampoo, soap, toothpaste etc',     'Lidl',    25.00, 15.00),
('Kitchen essentials',      'household', 80.00, 'Pots, pans, plates, cutlery',       'Tesco',   55.00, 25.00),
('Food starter shop',       'household',100.00, 'First big grocery shop',             'Lidl',    75.00, 25.00);