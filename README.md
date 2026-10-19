# Recipe Site Backend

This is the Express.js backend for a recipe sharing social network. It handles user accounts, recipe data, reviews, follows, and personalized feeds.

## Features

- User sign up, sign in, sign out, and profile access
- User management with role and name-based queries
- Recipe creation, retrieval, and deletion
- Review creation, retrieval, and deletion
- User following/follower relationships
- Feed endpoints for recipes and reviews from followed users
- MongoDB persistence using Mongoose

## Tech Stack

- Node.js
- Express.js
- MongoDB + Mongoose

## Project Structure

```text
.
├── index.js                 # Express app bootstrap and middleware setup
├── package.json             # Project metadata and scripts
├── Site/
│   ├── Recipes/
│   │   ├── routes.js        # Recipe API endpoints
│   │   └── schema.js        # Recipe schema definition
│   ├── Reviews/
│   │   ├── routes.js        # Review API endpoints
│   │   └── schema.js        # Review schema definition
│   └── Users/
│       ├── dao.js           # Data access layer for user/recipe/review logic
│       ├── model.js         # Mongoose model export
│       ├── routes.js        # User/auth API endpoints
│       └── schema.js        # User schema definition
└── .env                     # Local environment variables (not committed by default)
```

## API Overview

### Users

| Route                                              | Action                                            |
| -------------------------------------------------- | ------------------------------------------------- |
| `POST /api/users`                                  | Create user                                       |
| `POST /api/users/signUp`                           | Sign up                                           |
| `POST /api/users/signIn`                           | Sign in                                           |
| `POST /api/users/signOut`                          | Sign out                                          |
| `POST /api/users/profile`                          | Retrieves the session details of the current user |
| `GET /api/users`                                   | Get all users                                     |
| `GET /api/users/:userId`                           | Get user by ID                                    |
| `PUT /api/users/:userId`                           | Update user                                       |
| `DELETE /api/users/:userId`                        | Delete user                                       |
| `PUT /api/users/follow/:following/:followee`       | Follow                                            |
| `PUT /api/users/unfollow/:unfollowing/:unfollowee` | Unfollow                                          |

### Recipes

| Route                                | Action                              |
| ------------------------------------ | ----------------------------------- |
| `GET /api/recipes`                   | Get all recipes made by users       |
| `GET /api/recipes/following/:userId` | Get all recipes by users you follow |
| `PUT /api/recipes/create`            | Create recipe                       |
| `PUT /api/recipes/delete/:recipeId`  | Delete recipe                       |

### Reviews

| Route                                | Action                                    |
| ------------------------------------ | ----------------------------------------- |
| `GET /api/reviews`                   | Get all reviews                           |
| `GET /api/reviews/:reviewId`         | Get review by ID                          |
| `GET /api/reviews/api/:recipeId`     | Get all reviews for external recipe       |
| `GET /api/reviews/local/:recipeId`   | Get all reviews for recipe made by a user |
| `GET /api/reviews/following/:userId` | Get all reviews by users you follow       |
| `PUT /api/reviews/create`            | Create review                             |
| `PUT /api/reviews/delete/:reviewId`  | Delete review                             |

## Notes

The backend stores recipe and review data within user documents in MongoDB, rather than using separate collections for each entity.
