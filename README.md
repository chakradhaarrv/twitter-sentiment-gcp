# Twitter Sentiment Analysis Deployment

A real-time Twitter sentiment analysis web application deployed on Google Cloud Platform (GCP) and Heroku. This project analyzes the sentiment of tweets for any user-specified topic, providing instant feedback on whether the overall sentiment is positive, negative, or neutral.

## 🎯 Project Overview

This project simulates a real-world ML model deployment process, comparing deployment experiences across different cloud platforms. The application uses a real-time model serving approach with the Twitter API to instantly analyze sentiment from a specified number of tweets about any topic.

### Live Deployments

- **Google Cloud Platform**: https://twitter-sentiment-rdnwcv.uc.r.appspot.com/
- **Heroku**: https://twitter-sentiment-rdcvnw.herokuapp.com/

## 🚀 Features

- **Real-Time Analysis**: Instantly analyzes tweets as they're fetched from Twitter
- **Custom Topic Search**: Search for any topic or keyword
- **Configurable Sample Size**: Choose the number of tweets to analyze
- **Sentiment Classification**: Categorizes overall sentiment as Positive, Negative, or Neutral
- **Percentage Breakdown**: Calculates the percentage distribution of sentiments
- **Dual Deployment**: Available on both GCP and Heroku for comparison

## 🛠️ Technology Stack

- **Backend Framework**: Flask (Python 3.7)
- **Twitter Integration**: Tweepy - Python library for Twitter API access
- **Sentiment Analysis**: TextBlob - Natural language processing library
- **Cloud Platforms**: 
  - Google Cloud Platform (App Engine)
  - Heroku
- **Secret Management**: Google Cloud Secret Manager (for GCP deployment)
- **Additional Libraries**: NumPy, Matplotlib

## 📊 How It Works

1. **User Input**: User specifies a topic and the number of tweets to analyze
2. **Tweet Retrieval**: Application uses Tweepy to fetch tweets via Twitter API
3. **Sentiment Analysis**: TextBlob analyzes the polarity of each tweet:
   - **Positive**: Polarity > 0
   - **Negative**: Polarity < 0
   - **Neutral**: Polarity = 0
4. **Aggregation**: Calculates percentages and overall sentiment
5. **Result Display**: Shows the dominant sentiment on the web interface

## 🔧 Setup & Installation

### Prerequisites

- Python 3.7+
- Twitter Developer Account (for API credentials)
- Google Cloud account (for GCP deployment) or Heroku account

### Getting Twitter API Credentials

1. Sign up for a [Twitter Developer Account](https://developer.twitter.com/)
2. Create a new app in the developer portal
3. Generate your credentials:
   - Consumer Key (API Key)
   - Consumer Secret (API Secret)
   - Access Token
   - Access Token Secret

**Note**: Account approval may take a few days.

### Local Installation

```bash
# Clone the repository
git clone https://github.com/chakradhaarrv/twitter-sentiment-gcp.git
cd twitter-sentiment-gcp

# Install dependencies
pip install -r requirements.txt

# Set environment variables (or use .env file)
export CKey="your_consumer_key"
export CSecret="your_consumer_secret"
export AToken="your_access_token"
export ASecret="your_access_token_secret"

# Run the application
python main.py
```

Access the application at `http://localhost:5000`

## ☁️ Deployment

### Google Cloud Platform (App Engine)

1. Install [Google Cloud SDK](https://cloud.google.com/sdk/docs/install)
2. Initialize your GCP project:
   ```bash
   gcloud init
   gcloud app create
   ```
3. Store API credentials in Secret Manager:
   ```bash
   echo -n "your_consumer_key" | gcloud secrets create CKey --data-file=-
   echo -n "your_consumer_secret" | gcloud secrets create CSecret --data-file=-
   echo -n "your_access_token" | gcloud secrets create AToken --data-file=-
   echo -n "your_access_token_secret" | gcloud secrets create ASecret --data-file=-
   ```
4. Deploy the application:
   ```bash
   gcloud app deploy
   ```

### Heroku

1. Install [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli)
2. Login and create app:
   ```bash
   heroku login
   heroku create your-app-name
   ```
3. Set environment variables:
   ```bash
   heroku config:set CKey="your_consumer_key"
   heroku config:set CSecret="your_consumer_secret"
   heroku config:set AToken="your_access_token"
   heroku config:set ASecret="your_access_token_secret"
   ```
4. Deploy:
   ```bash
   git push heroku main
   ```

## 📁 Project Structure

```
twitter-sentiment-gcp/
├── main.py                 # Flask application and sentiment analysis logic
├── app.yaml               # GCP App Engine configuration
├── requirements.txt       # Python dependencies
├── README.md             # Project documentation
├── static/
│   └── style.css         # Frontend styling
└── templates/
    └── index.html        # Web interface
```

## 🔍 Key Components

### Sentiment Analysis Process

```python
# For each tweet:
analysis = TextBlob(tweet.text)
polarity = analysis.sentiment.polarity

# Classification:
# polarity > 0  → Positive
# polarity < 0  → Negative
# polarity == 0 → Neutral
```

### Percentage Calculation

```python
def percentage(part, whole):
    return 100 * float(part)/float(whole)
```

## 📈 Platform Comparison

| Feature | Google Cloud Platform | Heroku |
|---------|----------------------|---------|
| Setup Complexity | Moderate (Secret Manager required) | Simple (Config vars) |
| Scalability | Excellent (Auto-scaling) | Good |
| Free Tier | Available | Available (with limitations) |
| Deployment Speed | Fast | Very Fast |
| Secret Management | Built-in (Secret Manager) | Environment Variables |

## 🔒 Security

- API credentials stored as secrets (GCP Secret Manager) or environment variables (Heroku)
- No hardcoded credentials in source code
- Credentials excluded from version control

## ⚠️ Limitations

- Twitter API rate limits apply (varies by account type)
- Free tier deployments may have cold start delays
- Analysis limited to English language tweets
- Developer account approval required

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📝 License

This project is part of the UIC IDS594 Machine Learning Deployment course.

## 🙏 Acknowledgments

- **Tweepy**: Simplified Twitter API access and tweet streaming
- **TextBlob**: Easy-to-use sentiment analysis capabilities
- **UIC IDS594**: Machine Learning Deployment course project

## 📧 Contact

For questions or feedback, please open an issue on GitHub.

---

**Course**: IDS594 - Machine Learning Deployment, University of Illinois Chicago
