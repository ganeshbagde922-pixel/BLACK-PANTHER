import pandas as pd
from textblob import TextBlob
import seaborn as sns
import matplotlib.pyplot as plt

# Load the data
data = pd.read_csv("black_panther_reviews.csv")

# Function to get sentiment polarity
def get_sentiment(text):
    sentiment = TextBlob(text).sentiment.polarity
    if sentiment > 0:
        return "Positive"
    elif sentiment < 0:
        return "Negative"
    else:
        return "Neutral"

# Apply function
data["Sentiment"] = data["Review"].apply(get_sentiment)

# Print table
print("\n🎬 Black Panther Sentiment Analysis\n")
print(data)

# Plot sentiment distribution
plt.figure(figsize=(6,5))
sns.countplot(x="Sentiment", data=data, palette="viridis")
plt.title("Audience Sentiment towards 'Black Panther'")
plt.xlabel("Sentiment")
plt.ylabel("Number of Reviews")
plt.show()

# Summary
positive = (data["Sentiment"] == "Positive").sum()
negative = (data["Sentiment"] == "Negative").sum()
neutral = (data["Sentiment"] == "Neutral").sum()

print("\n📊 Summary:")
print(f"Positive: {positive}")
print(f"Negative: {negative}")
print(f"Neutral: {neutral}")
