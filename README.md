# Instagram Scraping with Instaloader

Welcome to the Instagram Scraping repository! This project utilizes the **Instaloader** library to gather information about Instagram profiles, including user details, posts, followers, and followees. Whether you want to explore your own profile or analyze someone else's, this script provides a foundation for Instagram scraping.

## Table of Contents
- [Installation](#installation)
- [Usage](#usage)
  - [Profile Information](#profile-information)
  - [Downloading Posts](#downloading-posts)
  - [Finding Non-Followers](#finding-non-followers)
- [Disclaimer](#disclaimer)
- [Contributing](#contributing)
- [License](#license)

## Installation

Make sure you have **Instaloader** installed. You can install it using:

```bash
pip install instaloader
```

## Usage

### Profile Information

```python
# Import the module
import instaloader

# Create an instance of Instaloader class
bot = instaloader.Instaloader()

# Load a profile from an Instagram handle
profile = instaloader.Profile.from_username(bot.context, 'mzaid295')

# Print profile information
print("Username: ", profile.username)
print("User ID: ", profile.userid)
print("Number of Posts: ", profile.mediacount)
print("Followers: ", profile.followers)
print("Following: ", profile.followees)
print("Bio: ", profile.biography, profile.external_url)
```

### Downloading Posts

```python
# Load a new profile
profile = instaloader.Profile.from_username(bot.context, 'chzaid295')

# Get all posts in a generator object
posts = profile.get_posts()

# Iterate and download
for index, post in enumerate(posts, 1):
    bot.download_post(post, target=f"{profile.username}_{index}")
```

### Finding Non-Followers

```python
import instaloader

def get_non_followers(username, password):
    # Create an instance of Instaloader
    loader = instaloader.Instaloader()

    try:
        # Login to Instagram account
        loader.login(username, password)

        # Get the profile of the logged-in user
        profile = instaloader.Profile.from_username(loader.context, username)

        # Get the following and followers
        following = set(profile.get_followees())
        followers = set(profile.get_followers())

        # Find users who don't follow back
        non_followers = following - followers

        # Print non-followers' usernames
        for user in non_followers:
            print(user.username)

    except instaloader.exceptions.InstaloaderException as e:
        print(f"An error occurred: {str(e)}")

# Replace 'your_username' and 'your_password' with your Instagram credentials
get_non_followers('your_username', 'your_password')
```

## Disclaimer

Please be aware that web scraping may violate the terms of service of some websites, including Instagram. Ensure you comply with Instagram's policies before using this tool. Use this script responsibly and respect the privacy and rights of others.

## Contributing

Feel free to contribute to this project by forking the repository and submitting pull requests. Bug reports, feature requests, and feedback are always welcome.

## License

This project is licensed under the [MIT License](LICENSE).
