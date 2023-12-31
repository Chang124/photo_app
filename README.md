#Dabase structure 

-- Account table
CREATE TABLE `photo_app`.`accounts` (
`userId` INT(11) NOT NULL AUTO_INCREMENT , 
`firstName` VARCHAR(50) NOT NULL , 
`lastName` VARCHAR(50) NOT NULL , 
`email` VARCHAR(50) NOT NULL , 
`password` VARCHAR(255) NOT NULL , 
`role` VARCHAR(20) NOT NULL DEFAULT 'User' , 
`avatar` VARCHAR(255) NOT NULL , 
`date` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP, 
PRIMARY KEY (`userId`)) ENGINE = InnoDB;

-- Album 
CREATE TABLE `photo_app`.`album` (
`albumId` INT(11) NOT NULL AUTO_INCREMENT , 
`userId` INT(11) NOT NULL , 
`albumName` VARCHAR(50) NOT NULL, 
FOREIGN KEY (`userId`) REFERENCES `account`(`userId`) ON DELETE RESTRICT ON UPDATE RESTRICT),
PRIMARY KEY (`albumId`)) ENGINE = InnoDB;

-- Category
CREATE TABLE `photo_app`.`category` (
`cateID` INT(11) NOT NULL AUTO_INCREMENT , 
`cateName` VARCHAR(20) NOT NULL, 
`date` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP, 
PRIMARY KEY (`cateID`)) ENGINE = InnoDB;

-- Photo
CREATE TABLE `photo_app`.`photo` (
`photoId` INT(11) NOT NULL AUTO_INCREMENT , 
`userId` INT(11) NOT NULL , 
`caption` VARCHAR(100) NOT NULL , 
`description` VARCHAR(225) NOT NULL , 
`category` INT(11) NOT NULL , 
`photoPath` VARCHAR(255) NOT NULL , 
`updateDate` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP , 
`album` INT(11) NOT NULL , 
PRIMARY KEY (`photoId`)) ENGINE = InnoDB;
ALTER TABLE `photo` ADD FOREIGN KEY (`album`) REFERENCES `album`(`albumId`) ON DELETE RESTRICT ON UPDATE RESTRICT;
ALTER TABLE `photo` ADD FOREIGN KEY (`userId`) REFERENCES `account`(`userId`) ON DELETE RESTRICT ON UPDATE RESTRICT;
ALTER TABLE `photo` ADD FOREIGN KEY (`category`) REFERENCES `category`(`cateID`) ON DELETE RESTRICT ON UPDATE RESTRICT;

-- Comment
CREATE TABLE `photo_app`.`comment` (
`cmtID` INT(11) NOT NULL AUTO_INCREMENT , 
`photoId` INT(11) NOT NULL , 
`userId` INT(11) NOT NULL , 
`content` VARCHAR(255) NOT NULL , 
`date` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP, 
PRIMARY KEY (`cmtID`)) ENGINE = InnoDB;
ALTER TABLE `comment` ADD FOREIGN KEY (`userId`) REFERENCES `account`(`userId`) ON DELETE RESTRICT ON UPDATE RESTRICT; 
ALTER TABLE `comment` ADD FOREIGN KEY (`photoId`) REFERENCES `photo`(`photoId`) ON DELETE RESTRICT ON UPDATE RESTRICT;
