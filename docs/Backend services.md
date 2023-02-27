<h1 align="center"><b> Backend services </b></h1>

<h2> <u> Documentation for AuthService: </u></h2>

This class handles authentication-related functionality for the system.

<b>Methods:</b>

- Register(AuthRegisterRequest request): This method creates a new user account by taking AuthRegisterRequest object as an input parameter. It checks if the email already exists and throws an exception if it does. Then it creates a new Auth object, sends a token if in RELEASE mode, and saves the Auth object to the database. The method returns the Auth object.
- Login(AuthLoginRequest request): This method logs in a user by taking AuthLoginRequest object as an input parameter. It retrieves the Auth object based on the provided email, and verifies the password. If the password is correct, it generates a JWT token and returns it.
- Verify(string token): This method verifies the user account by taking a token as an input parameter. It retrieves the Auth object based on the provided token, updates the verification date, and returns the Auth object.
- ForgotPassword(string email): This method initiates the password reset process by taking an email as an input parameter. It retrieves the Auth object based on the provided email, sets the reset token and its expiration time, and returns the Auth object.
- ResetPassword(AuthResetPasswordRequest request): This method resets the user's password by taking AuthResetPasswordRequest object as an input parameter. It retrieves the Auth object based on the provided token, checks if the token is valid, and updates the Auth object with the new password. The method returns the Auth object.

<b>Exceptions:</b>

- "Username or password is not correct!" - Thrown when a user tries to login with an incorrect username or password.
- "Email already exists." - Thrown when a user tries to register with an email address that already exists in the database.
- "Not verified! Check your emails and verify your account!" - Thrown when a user tries to login but their account has not been verified.
- "Invalid token!" - Thrown when a user tries to verify their account with an invalid token.
- "User not found!" - Thrown when a user tries to reset their password, but there is no user associated with the provided email address.
- "Invalid Token!" - Thrown when a user tries to reset their password with an invalid token.
- "Invalid password!" - Thrown when a user tries to set a password that is too short or too long.
- "Empty auth." - Thrown when an empty Auth object is passed to a method that requires it.
- "Invalid username." - Thrown when an Auth object has an invalid username.
- "Invalid email." - Thrown when an Auth object has an invalid email address.
- "Invalid email!" - Thrown when a user tries to register with an invalid email address.
- "Invalid confirm password!" - Thrown when a user tries to register with a password that doesn't match the confirmation password.

<h2> <u> Documentation for FoodService:</u></h2>

This class handles food-related functionality for the system.

<b>Methods:</b>

- GetRecommendedTags(int foodId): This method retrieves a list of recommended tags for a given food item by taking the food ID as an input parameter. It checks if the food exists and retrieves a list of tags that are marked as recommended. The method returns the list of tags.
- AddTags(AddTagsToFoodRequest request): This method adds tags to a given food item by taking AddTagsToFoodRequest object as an input parameter. It checks if the food item exists and retrieves the tags to be added. It then creates a new FoodsHaveTags object for each tag and adds it to the database. The method returns the updated Food object.
- Create(FoodCreateRequest request): This method creates a new food item by taking FoodCreateRequest object as an input parameter. It creates a new Food object, sets its attributes, and verifies the data. It then adds the Food object to the database and returns it.
- Delete(int id): This method deletes a food item by taking its ID as an input parameter. It checks if the food item exists and deletes it from the database.
- Update(FoodUpdateRequest request): This method updates a food item by taking FoodUpdateRequest object as an input parameter. It retrieves the food item based on the provided ID, updates its attributes, and verifies the data. It then updates the Food object in the database and returns it.
- VerifyUnVerify(int id): This method verifies or unverifies a food item by taking its ID as an input parameter. It retrieves the food item based on the provided ID, updates its verification status, and updates the Food object in the database. The method returns the updated Food object.

<b>Exceptions:</b>

- "Food (id:{foodId}) does not exist." - Thrown when a food with the given ID does not exist in the database while trying to get its recommended tags.
- "This food doesn't exist." - Thrown when a food with the given ID does not exist in the database while trying to add tags, update, or verify/unverify a food.
- "This tag ($id={tagId}) doesn't exist." - Thrown when a tag with the given ID does not exist in the database while trying to add tags to a food.
- "This food already have this tag." - Thrown when a food already has the same tag while trying to add tags to a food.
- "Name can't be longer than 50 characters!" - Thrown when a food name has more than 50 characters while creating or updating a food.
- "Please enter at least 5 characters to the name field." - Thrown when a food name has less than 5 characters while creating or updating a food.
- "100g food can't contain more than 100g fat." - Thrown when the food contains more than 100g fat per 100g while creating or updating a food.
- "100g food can't contain more than 100g protein." - Thrown when the food contains more than 100g protein per 100g while creating or updating a food.
- "100g food can't contain more than 100g carbohydrate." - Thrown when the food contains more than 100g carbohydrate per 100g while creating or updating a food.
- "Food can't contain less than 0g fat." - Thrown when the food contains less than 0g fat while creating or updating a food.
- "Food can't contain less than 0g protein." - Thrown when the food contains less than 0g protein while creating or updating a food.
- "Food can't contain less than 0g carbohydrate." - Thrown when the food contains less than 0g carbohydrate while creating or updating a food.
- "Food can't contain less than 0kcal." - Thrown when the food contains less than 0kcal while creating or updating a food.

<h2> <u> Documentation for OilService:</u></h2>

The OilService class provides CRUD operations for the Oil entity. 

<b>Methods:</b>

- Create(OilCreateRequest request): This method creates a new oil object with the specified name and calorie count in 14ml, validates the input data, and returns the created oil object.
- Update(OilUpdateRequest request): This method updates the oil object with the specified id, validates the input data, and returns the updated oil object.
- Delete(int id): This method deletes the oil object with the specified id.

<b>Exceptions:</b>

- "Oil object is null." - Thrown when an Oil object passed to the CheckData() method is null.
- "Name can't be longer than 50 characters!" - Thrown when the name property of an Oil object is longer than 50 characters.
- "Oils can't contain more than 300 cal/14ml!" - Thrown when the calIn14Ml property of an Oil object is greater than 300.
- "Please enter at least 5 characters to the name field." - Thrown when the name property of an Oil object is less than 5 characters.
- "Oils can't contain less than 30 cal/14ml!" - Thrown when the calIn14Ml property of an Oil object is less than 30.
- "This oil doesn't exist." - Thrown when the Oil object returned by the Read() method of the GenericService class is null.

<h2> <u> Documentation for RecipeService:</u></h2>

The RecipeService class provides CRUD operations for the Recipe entity. 

<b>Methods:</b>

- WriteRecipe(WriteRecipeRequest request): This method creates a new recipe object with the specified author, name, method, time, and ingredients, calculates the nutritional values and generates a description for the recipe, validates the input data, and returns the created recipe object.
- Update(UpdateRecipeRequest request): This method updates the recipe object with the specified id, author, name, method, time, and ingredients, calculates the nutritional values and generates a description for the recipe, validates the input data, and returns the updated recipe object.
- Delete(int recipeId): This method deletes the recipe object with the specified id.

<b>Exceptions:</b>

- "This recipe doesn't exist." - This exception is thrown when an attempt is made to read, update or delete a recipe that doesn't exist in the database.
- "Only the author can delete the recipe." - This exception is thrown when a user who is not the author of the recipe tries to delete it.
- "Some ingredient has no portion." - This exception is thrown when the number of ingredients is not equal to the number of ingredient portions.
- "You need to choose an oil, if you fry something." - This exception is thrown when a user tries to fry something without selecting an oil.
- "Oil has no portion!" - This exception is thrown when a user tries to fry something without specifying the quantity of oil.
- "Only the author can modify the recipe, please check in the "save as" option, if you want to create a new recipe base on this one!" - This exception is thrown when a user who is not the author of the recipe tries to modify it without selecting the "save as" option. This option creates a new recipe based on the original recipe.
- "Some ingredient has no portion." - This exception is thrown when the number of ingredients is not equal to the number of ingredient portions.
- "Recipe name is empty." - This exception is thrown when a user tries to update a recipe without specifying a name for it.
- "Method is not defined." - This exception is thrown when a user tries to update a recipe without specifying a preparation method.
- "Ingredient or portion missing." - This exception is thrown when a user tries to update a recipe without specifying an ingredient or its corresponding portion.

<h2> <u> Documentation for SocialMediaService:</u></h2>

The SocialMediaService class provides methods for commenting, following/unfollowing users, and retrieving comments for a specific user. 

<b>Methods:</b>

- ModifyComment(ModifyCommentRequest request) This method modifies the body of a comment made by the authenticated user. It takes a ModifyCommentRequest object as a parameter, which contains the comment ID and the new body. It returns a Comment object that represents the modified comment. If the comment doesn't exist or the authenticated user is not the author of the comment, an exception will be thrown.
- CreateCommentListByAuthenticatedEmail: This method retrieves a list of comments directed to the authenticated user. It returns a List of Comment objects. If the authenticated user doesn't exist or there are no comments for the user, an empty list will be returned.
- DeleteCommentById(int commentId): This method deletes a comment made by the authenticated user. It takes the ID of the comment as a parameter. If the comment doesn't exist or the authenticated user is not the author or recipient of the comment, an exception will be thrown.
- StartOrStopFollow(UnFollowFollowRequest request): This method allows the authenticated user to follow or unfollow another user. It takes an UnFollowFollowRequest object as a parameter, which contains the email address of the user to follow/unfollow. If the user to follow/unfollow doesn't exist or the authenticated user is attempting to follow themselves, an exception will be thrown.
- SendComment(WriteCommentRequest request) This method allows the authenticated user to send a comment to another user. It takes a WriteCommentRequest object as a parameter, which contains the email address of the recipient and the comment body. It returns a Comment object that represents the sent comment. If the recipient user doesn't exist, an exception will be thrown.

<b>Exceptions:</b>

- "Comment doesn't exist." - Thrown when a comment with the specified ID doesn't exist. 
- "You do not have permission to modify the comment." - Thrown when the authenticated user does not have permission to modify the specified comment.
- ` `"You do not have permission to delete the comment." - Thrown when the authenticated user does not have permission to delete the specified comment. 
- "Auth to follow doesn't exist." - Thrown when an Auth object with the specified email address doesn't exist. 
- "You need to create a user profile first!" - Thrown when the authenticated user doesn't have a user profile and tries to perform an action that requires one. 
- "Invalid 'toAuth' email." - Thrown when an invalid email address is passed to the SendComment method. 
- "'toAuth' doesn't exist." - Thrown when an Auth object with the specified email address doesn't exist in the SendComment method. 
- "Invalid 'toAuth' username." - Thrown when an Auth object has an invalid username in the SendComment method. 
- "'toAuth' has no user profile!" - Thrown when the user profile for the specified Auth object doesn't exist in the SendComment method. 
- "You can't follow yourself." - Thrown when the authenticated user tries to follow their own user profile in the StartOrStopFollow method.

Note: The authenticated user must have a user profile in the system to use these methods.

<h2> <u> Documentation for TagService:</u></h2>

The TagService class provides CRUD operations for the Tag entity. 

<b>Methods:</b>

- Create(TagCreateRequest request): This method creates a new tag object with the specified name, description, food property, maximum value, and minimum value. It checks the input data for validity and returns the created tag object.
- Update(TagUpdateRequest request): This method updates the tag object with the specified id, name, and description. It checks the input data for validity and returns the updated tag object.
- Delete(int id): This method deletes the tag object with the specified id. If the tag object does not exist, an exception is thrown.

<b>Exceptions:</b>

- "Name can't be longer than 50 character!" - Thrown when the length of the name property of the Tag object passed to the CheckData method is greater than 50 characters.
- "Description can't be longer than 500 character!" - Thrown when the length of the description property of the Tag object passed to the CheckData method is greater than 500 characters.
- "Please enter at least 3 character to the name field." - Thrown when the length of the name property of the Tag object passed to the CheckData method is less than 3 characters.
- "Please enter at least 10 character to the description field." - Thrown when the length of the description property of the Tag object passed to the CheckData method is less than 10 characters.
- "You can't give value to min or max, if you don't choose a property." - Thrown when the foodProperty property of the Tag object passed to the CheckData method is null and either the min or max properties are not null.
- "Please enter a number between 0 and 100 to do max field!" - Thrown when the value of the max property of the Tag object passed to the CheckData method is not between 0 and 100.
- "Please enter a number between 0 and 100 to do min field!" - Thrown when the value of the min property of the Tag object passed to the CheckData method is not between 0 and 100.
- "This tag doesn't exist." - Thrown when the Tag object with the specified id does not exist in the database.

<h2> <u> Documentation for UserProfileService:</u></h2>

The UserProfileService class provides operations for managing user profiles.

<b>Methods:</b>

- SetProfilePicture(UserSetProfilePictureRequset request): This method updates the user profile picture with the specified hair, skin, eyes, and mouth indices. It checks the input data for validity and returns the updated user profile object.
- CreateProfile(UserSetDatasRequest request): This method creates a new user profile object with the specified weight, height, birth date, gender, and goal weight. If the goal weight is not specified, it is automatically set based on the user's height and weight. It checks the input data for validity and returns the created user profile object.
- ModifyProfile(UserSetDatasRequest request): This method updates the user profile object with the specified weight, height, birth date, gender, and goal weight. If any of the fields are not specified, their values are not changed. If the goal weight is not specified, it is automatically set based on the user's height and weight. It checks the input data for validity and returns the updated user profile object.

<b>Exceptions:</b>

- "You must log in first." - Thrown when auth is null in the constructor of UserProfileService.
- "The user must be between 12 and 100 years old!" - Thrown when the user's age is less than 12 or greater than 100 in CheckCreateRequest and CheckUpdateRequest methods.
- "The user weight must be over 20 and 1000!" - Thrown when the user's weight is less than 20 or greater than 1000 in CheckCreateRequest and CheckUpdateRequest methods.
- "The user height must be between 40 and 250 cm!" - Thrown when the user's height is less than 40 or greater than 250 in CheckCreateRequest and CheckUpdateRequest methods.
- "You must select your gender!" - Thrown when the user's gender is nondefined in CheckCreateRequest method.
- "Invalid gender!" - Thrown when the user's gender is less than nondefined or greater than other in CheckCreateRequest and CheckUpdateRequest methods.
- "The user goal weight must be over 20 and 1000!" - Thrown when the user's goal weight is less than 20 or greater than 1000 in CheckCreateRequest and CheckUpdateRequest methods.
- "Invalid hair!" - Thrown when the user's hairIndex is less than nondefined or greater than white in CheckProfilePicture method.
- "Invalid skin color!" - Thrown when the user's skinIndex is less than nondefined or greater than lightest in CheckProfilePicture method.
- "Invalid eye color!" - Thrown when the user's eyesIndex is less than nondefined or greater than brown in CheckProfilePicture method.
- "Invalid mouth!" - Thrown when the user's mouthIndex is less than nondefined or greater than smiling in CheckProfilePicture method.