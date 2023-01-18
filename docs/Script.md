CREATE TABLE IF NOT EXISTS `__EFMigrationsHistory` (
    `MigrationId` varchar(150) CHARACTER SET utf8mb4 NOT NULL,
    `ProductVersion` varchar(32) CHARACTER SET utf8mb4 NOT NULL,
    CONSTRAINT `PK___EFMigrationsHistory` PRIMARY KEY (`MigrationId`)
) CHARACTER SET=utf8mb4;

START TRANSACTION;

ALTER DATABASE CHARACTER SET utf8mb4;

CREATE TABLE `auths` (
    `id` int NOT NULL AUTO_INCREMENT,
    `username` longtext CHARACTER SET utf8mb4 NOT NULL,
    `email` longtext CHARACTER SET utf8mb4 NOT NULL,
    `passwordHash` longblob NOT NULL,
    `passwordSalt` longblob NOT NULL,
    `isAdmin` tinyint(1) NOT NULL,
    `verificationToken` longtext CHARACTER SET utf8mb4 NULL,
    `date` datetime(6) NULL,
    `passwordResetToken` longtext CHARACTER SET utf8mb4 NULL,
    `resetTokenExpires` datetime(6) NULL,
    CONSTRAINT `PK_auths` PRIMARY KEY (`id`)
) CHARACTER SET=utf8mb4;

CREATE TABLE `oils` (
    `id` int NOT NULL AUTO_INCREMENT,
    `kcalIn14Ml` int NOT NULL,
    CONSTRAINT `PK_oils` PRIMARY KEY (`id`)
) CHARACTER SET=utf8mb4;

CREATE TABLE `userProfiles` (
    `id` int NOT NULL AUTO_INCREMENT,
    `weight` double NOT NULL,
    `height` double NOT NULL,
    `birthDate` longtext CHARACTER SET utf8mb4 NOT NULL,
    `gender` int NOT NULL,
    `goalWeight` double NOT NULL,
    `hairIndex` int NOT NULL,
    `skinIndex` int NOT NULL,
    `eyesIndex` int NOT NULL,
    `mouthIndex` int NOT NULL,
    `authOfProfileId` int NOT NULL,
    CONSTRAINT `PK_userProfiles` PRIMARY KEY (`id`),
    CONSTRAINT `FK_userProfiles_auths_authOfProfileId` FOREIGN KEY (`authOfProfileId`) REFERENCES `auths` (`id`) ON DELETE CASCADE
) CHARACTER SET=utf8mb4;

CREATE TABLE `comments` (
    `id` int NOT NULL AUTO_INCREMENT,
    `fromId` int NOT NULL,
    `toId` int NOT NULL,
    `body` varchar(1000) CHARACTER SET utf8mb4 NOT NULL,
    `sendDate` longtext CHARACTER SET utf8mb4 NOT NULL,
    CONSTRAINT `PK_comments` PRIMARY KEY (`id`),
    CONSTRAINT `FK_comments_userProfiles_fromId` FOREIGN KEY (`fromId`) REFERENCES `userProfiles` (`id`) ON DELETE RESTRICT,
    CONSTRAINT `FK_comments_userProfiles_toId` FOREIGN KEY (`toId`) REFERENCES `userProfiles` (`id`) ON DELETE RESTRICT
) CHARACTER SET=utf8mb4;

CREATE TABLE `followings` (
    `followerId` int NOT NULL,
    `followedId` int NOT NULL,
    `followDate` longtext CHARACTER SET utf8mb4 NOT NULL,
    CONSTRAINT `PK_followings` PRIMARY KEY (`followedId`, `followerId`),
    CONSTRAINT `FK_followings_userProfiles_followedId` FOREIGN KEY (`followedId`) REFERENCES `userProfiles` (`id`) ON DELETE RESTRICT,
    CONSTRAINT `FK_followings_userProfiles_followerId` FOREIGN KEY (`followerId`) REFERENCES `userProfiles` (`id`) ON DELETE RESTRICT
) CHARACTER SET=utf8mb4;

CREATE TABLE `last24Hs` (
    `id` int NOT NULL AUTO_INCREMENT,
    `kcal` int NOT NULL,
    `protein` int NOT NULL,
    `fat` int NOT NULL,
    `carbohydrate` int NOT NULL,
    `liquidInDl` int NOT NULL,
    `minLiquidInDl` int NOT NULL,
    `maxKcal` int NOT NULL,
    `userProfileId` int NOT NULL,
    CONSTRAINT `PK_last24Hs` PRIMARY KEY (`id`),
    CONSTRAINT `FK_last24Hs_userProfiles_userProfileId` FOREIGN KEY (`userProfileId`) REFERENCES `userProfiles` (`id`) ON DELETE CASCADE
) CHARACTER SET=utf8mb4;

CREATE TABLE `recipes` (
    `id` int NOT NULL AUTO_INCREMENT,
    `kcal` int NOT NULL,
    `protein` int NOT NULL,
    `fat` int NOT NULL,
    `carbohydrate` int NOT NULL,
    `name` longtext CHARACTER SET utf8mb4 NOT NULL,
    `verifeid` tinyint(1) NOT NULL,
    `Authorid` int NOT NULL,
    `oilId` int NULL,
    CONSTRAINT `PK_recipes` PRIMARY KEY (`id`),
    CONSTRAINT `FK_recipes_oils_oilId` FOREIGN KEY (`oilId`) REFERENCES `oils` (`id`),
    CONSTRAINT `FK_recipes_userProfiles_Authorid` FOREIGN KEY (`Authorid`) REFERENCES `userProfiles` (`id`) ON DELETE CASCADE
) CHARACTER SET=utf8mb4;

CREATE TABLE `foods` (
    `id` int NOT NULL AUTO_INCREMENT,
    `name` longtext CHARACTER SET utf8mb4 NOT NULL,
    `kcal` int NOT NULL,
    `protein` int NOT NULL,
    `fat` int NOT NULL,
    `carbohydrate` int NOT NULL,
    `last24hid` int NOT NULL,
    CONSTRAINT `PK_foods` PRIMARY KEY (`id`),
    CONSTRAINT `FK_foods_last24Hs_last24hid` FOREIGN KEY (`last24hid`) REFERENCES `last24Hs` (`id`) ON DELETE CASCADE
) CHARACTER SET=utf8mb4;

CREATE TABLE `tags` (
    `id` int NOT NULL AUTO_INCREMENT,
    `name` longtext CHARACTER SET utf8mb4 NOT NULL,
    `Recipeid` int NULL,
    CONSTRAINT `PK_tags` PRIMARY KEY (`id`),
    CONSTRAINT `FK_tags_recipes_Recipeid` FOREIGN KEY (`Recipeid`) REFERENCES `recipes` (`id`)
) CHARACTER SET=utf8mb4;

CREATE TABLE `UsersLikeRecipes` (
    `userId` int NOT NULL,
    `recipeId` int NOT NULL,
    `date` datetime(6) NOT NULL,
    CONSTRAINT `PK_UsersLikeRecipes` PRIMARY KEY (`userId`, `recipeId`),
    CONSTRAINT `FK_UsersLikeRecipes_recipes_userId` FOREIGN KEY (`userId`) REFERENCES `recipes` (`id`) ON DELETE RESTRICT,
    CONSTRAINT `FK_UsersLikeRecipes_userProfiles_recipeId` FOREIGN KEY (`recipeId`) REFERENCES `userProfiles` (`id`) ON DELETE RESTRICT
) CHARACTER SET=utf8mb4;

CREATE TABLE `RecipesIncludeIngredients` (
    `id` int NOT NULL AUTO_INCREMENT,
    `portionInGramm` int NOT NULL,
    `recipeId` int NOT NULL,
    `foodId` int NOT NULL,
    CONSTRAINT `PK_RecipesIncludeIngredients` PRIMARY KEY (`id`),
    CONSTRAINT `FK_RecipesIncludeIngredients_foods_foodId` FOREIGN KEY (`foodId`) REFERENCES `foods` (`id`) ON DELETE RESTRICT,
    CONSTRAINT `FK_RecipesIncludeIngredients_recipes_recipeId` FOREIGN KEY (`recipeId`) REFERENCES `recipes` (`id`) ON DELETE RESTRICT
) CHARACTER SET=utf8mb4;

CREATE TABLE `FoodsHaveTags` (
    `foodId` int NOT NULL,
    `tagId` int NOT NULL,
    CONSTRAINT `PK_FoodsHaveTags` PRIMARY KEY (`foodId`, `tagId`),
    CONSTRAINT `FK_FoodsHaveTags_foods_tagId` FOREIGN KEY (`tagId`) REFERENCES `foods` (`id`) ON DELETE RESTRICT,
    CONSTRAINT `FK_FoodsHaveTags_tags_foodId` FOREIGN KEY (`foodId`) REFERENCES `tags` (`id`) ON DELETE RESTRICT
) CHARACTER SET=utf8mb4;

CREATE TABLE `UsersPreferTags` (
    `userId` int NOT NULL,
    `tagId` int NOT NULL,
    CONSTRAINT `PK_UsersPreferTags` PRIMARY KEY (`userId`, `tagId`),
    CONSTRAINT `FK_UsersPreferTags_tags_userId` FOREIGN KEY (`userId`) REFERENCES `tags` (`id`) ON DELETE RESTRICT,
    CONSTRAINT `FK_UsersPreferTags_userProfiles_tagId` FOREIGN KEY (`tagId`) REFERENCES `userProfiles` (`id`) ON DELETE RESTRICT
) CHARACTER SET=utf8mb4;

CREATE INDEX `IX_comments_fromId` ON `comments` (`fromId`);

CREATE INDEX `IX_comments_toId` ON `comments` (`toId`);

CREATE INDEX `IX_followings_followerId` ON `followings` (`followerId`);

CREATE INDEX `IX_foods_last24hid` ON `foods` (`last24hid`);

CREATE INDEX `IX_FoodsHaveTags_tagId` ON `FoodsHaveTags` (`tagId`);

CREATE UNIQUE INDEX `IX_last24Hs_userProfileId` ON `last24Hs` (`userProfileId`);

CREATE INDEX `IX_recipes_Authorid` ON `recipes` (`Authorid`);

CREATE INDEX `IX_recipes_oilId` ON `recipes` (`oilId`);

CREATE INDEX `IX_RecipesIncludeIngredients_foodId` ON `RecipesIncludeIngredients` (`foodId`);

CREATE INDEX `IX_RecipesIncludeIngredients_recipeId` ON `RecipesIncludeIngredients` (`recipeId`);

CREATE INDEX `IX_tags_Recipeid` ON `tags` (`Recipeid`);

CREATE UNIQUE INDEX `IX_userProfiles_authOfProfileId` ON `userProfiles` (`authOfProfileId`);

CREATE INDEX `IX_UsersLikeRecipes_recipeId` ON `UsersLikeRecipes` (`recipeId`);

CREATE INDEX `IX_UsersPreferTags_tagId` ON `UsersPreferTags` (`tagId`);

INSERT INTO `__EFMigrationsHistory` (`MigrationId`, `ProductVersion`)
VALUES ('20221219101629_Initial', '6.0.10');

COMMIT;

START TRANSACTION;

ALTER TABLE `recipes` DROP COLUMN `verifeid`;

ALTER TABLE `oils` CHANGE `kcalIn14Ml` `calIn14Ml` int NOT NULL DEFAULT 0;

ALTER TABLE `tags` ADD `description` longtext CHARACTER SET utf8mb4 NOT NULL;

ALTER TABLE `oils` ADD `name` longtext CHARACTER SET utf8mb4 NOT NULL;

ALTER TABLE `foods` ADD `verifeid` tinyint(1) NOT NULL DEFAULT FALSE;

INSERT INTO `__EFMigrationsHistory` (`MigrationId`, `ProductVersion`)
VALUES ('20221220095147_OrganisationAndRename', '6.0.10');

COMMIT;

START TRANSACTION;

ALTER TABLE `foods` DROP FOREIGN KEY `FK_foods_last24Hs_last24hid`;

ALTER TABLE `foods` MODIFY COLUMN `last24hid` int NULL;

ALTER TABLE `foods` ADD CONSTRAINT `FK_foods_last24Hs_last24hid` FOREIGN KEY (`last24hid`) REFERENCES `last24Hs` (`id`);

INSERT INTO `__EFMigrationsHistory` (`MigrationId`, `ProductVersion`)
VALUES ('20221220100956_Nullable24H', '6.0.10');

COMMIT;

START TRANSACTION;

ALTER TABLE `tags` ADD `foodProperty` int NOT NULL DEFAULT 0;

ALTER TABLE `tags` ADD `max` int NOT NULL DEFAULT 0;

ALTER TABLE `tags` ADD `min` int NOT NULL DEFAULT 0;

INSERT INTO `__EFMigrationsHistory` (`MigrationId`, `ProductVersion`)
VALUES ('20221226101936_RecommendedTags', '6.0.10');

COMMIT;

