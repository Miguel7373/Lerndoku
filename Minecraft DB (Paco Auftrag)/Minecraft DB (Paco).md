```d
Table blocks {

id int [pk, increment]

name varchar(100) [not null, unique]

is_natural boolean [not null, default: false]

}

  

Table natural_blocks {

block_id int [pk]

biome varchar(100)

renewability boolean [default: false]

}

  
  

Table recipes {

id int [pk, increment]

output_block_id int [not null, unique]

output_quantity int [not null, default: 1]

}

  
  

Table recipe_ingredients {

recipe_id int [not null]

input_block_id int [not null]

quantity int [not null]

  

Indexes {

(recipe_id, input_block_id) [pk]

}

}

  
  

Table buildings {

id int [pk, increment]

name varchar(150) [not null]

description text

}

  

Table building_blocks {

building_id int

block_id int

quantity int [not null]

  

Indexes {

(building_id, block_id) [pk]

}

}

  

Ref: natural_blocks.block_id > blocks.id

  

Ref: recipes.output_block_id > blocks.id

Ref: recipe_ingredients.recipe_id > recipes.id

Ref: recipe_ingredients.input_block_id > blocks.id


Ref: building_blocks.building_id > buildings.id

Ref: building_blocks.block_id > blocks.id
````


![[Screenshot from 2025-11-24 09-15-55.png]]

Examle:

The **blocks** table should have all blocks in it that exist in Minecraft.

INSERT INTO blocks (name, is_natural) VALUES
('Stone', true),
('Quartz', true),
('Comperator', false)
('Redstone Ore', true),
('Redstone Dust', false),    
('Redstone Torch', false);
('Stick', true);

The **natural_blocks** table should be there for all blocks that are natural. You could also leave this away and solve it only with the boolean of the blocks table, but I thought showing where to find them could be interesting.

INSERT INTO natural_blocks (block_id, biome, renewability) VALUES
(1, 'Cave', true),   -- Stone
(2, 'Nether', true),-- Quartz
(3, 'Cave', true);   -- Redstone Ore
(6, 'Any', true);

The **recipes** table is where all the Minecraft recipes should be saved and put into another list of blocks that you need to craft the item.

INSERT INTO recipes (output_block_id, output_quantity) VALUES
(6, 1); -- Redstone Torch
(3, 1); -- Comperator

The **recipes** ingredients are what blocks a recipe needs.

INSERT INTO recipe_ingredients (recipe_id, input_block_id, quantity) VALUES
(1, 4, 1),  -- 1 Redstone Dust
(1, 6, 1);  -- 1 Stick

(2, 2, 1),  -- 1 Quartz
(2, 1, 3),  -- 3 Stone
(2, 5, 3);  -- 3 Redstone Torches

The tables below are what the user inputs, so the block list and the building it is.

INSERT INTO building_blocks (building_id, block_id, quantity) VALUES
(1, 2, 1),  -- 1 Comperator

INSERT INTO buildings (name, description) VALUES
('Comparator', 'Redstone comparator used for comparing signals');


The natural checks should be repeated as long as there are still non natural blocks












Ancible only the fist few chapters  (3)

