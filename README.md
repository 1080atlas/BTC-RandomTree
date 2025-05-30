# BTC-RandomTree

Project Goals
The goal of this project was to build a machine learning-based trading strategy for Bitcoin that mimics how a human trader might think: using signals, confidence levels, and managing risk. Instead of optimizing blindly for returns, the idea was to simulate how someone might actually trade — adapting over time, betting bigger when confident, and cutting losses when needed.

This project evolved through several versions, each adding a bit more realism and complexity to the strategy logic.

Strategy Progression
1. First Version: Simple ML + Fixed 10-Day Exit
What it did: Trained a model to predict whether BTC would go up over the next 10 days and took trades if the probability was over 0.5.

Exit: Always exited after 10 days.

Performance:

Return: 2.98x

Max Drawdown: -33.41%

Sharpe Ratio: 3.36

Win Rate: 69.6%

Takeaway: Strong results, but the drawdowns were brutal. Good proof-of-concept, but not really something you'd want to trade live.

2. Added Position Sizing Based on Confidence
What it did: Sized trades depending on how confident the model was. Low confidence = small position, high confidence = full position.

Performance:

Return: 1.58x

Max Drawdown: -3.01%

Sharpe Ratio: 4.02

Takeaway: This added realism by mimicking how a trader might scale into trades, but it watered down the returns. A much smoother equity curve, though.

3. Introduced a 5% Stop-Loss
What it did: Added a stop-loss so trades would automatically close if they dropped 5% below the entry.

Performance:

Return: 1.79x

Max Drawdown: -18.68%

Sharpe Ratio: 3.55

Takeaway: This added much-needed downside protection, but it also cut off some trades too early. A decent middle ground between risk and return.

4. Walk-Forward Training (Rolling Retrain)
What it did: Simulated real-world trading by retraining the model every 30 days on the past year of data. This avoids lookahead bias and adapts to changing markets.

Performance:

Return: 3.54x

Max Drawdown: -20.06%

Sharpe Ratio: 5.90

Takeaway: The best overall result. It kept returns high while improving the Sharpe ratio a lot. Walk-forward training made the model more robust over time.

5. Dynamic Exit Based on Daily Confidence
What it did: Instead of setting a fixed exit, the model re-checked confidence daily and exited the trade early if confidence dropped below 0.5.

Performance:

Return: 1.14x

Max Drawdown: -8.54%

Sharpe Ratio: 3.54

Takeaway: Sounded great in theory but didn’t work well in practice. The model’s confidence was too noisy day-to-day, leading to lots of premature exits. The idea has potential, but it needs smoothing or additional rules.

Final Thoughts:

The first version proved the concept but wasn’t safe to trade without risk controls.

Confidence-based sizing and stop-losses helped manage risk, though sometimes at the cost of performance.

The walk-forward approach was the clear winner — it adapted to market changes and gave the best Sharpe ratio.

Dynamic exits based on confidence need more work. Confidence wasn’t stable enough for reliable daily decisions, at least not without some smoothing or averaging. Fixing this would also add a level of complexity where it felt out of my depth at this point. 
