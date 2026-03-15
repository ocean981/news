# news
import ycnbc
from datetime import datetime

def get_us_market_news():
    """获取美国市场新闻和数据"""
    
    # 初始化新闻和市场的API
    news = ycnbc.News()
    markets = ycnbc.Markets()
    
    print("=" * 60)
    print(f"📊 美国市场监控 - {datetime.now().strftime('%Y-%m-%d %H:%M')}")
    print("=" * 60)
    
    # 1. 获取美股市场概况
    print("\n🔹 美股市场指数:")
    us_markets = markets.us_markets()
    for market in us_markets[:5]:  # 显示前5个
        print(f"   {market['name']}: {market.get('value', 'N/A')} "
              f"({market.get('change', 'N/A')})")
    
    # 2. 获取热门新闻
    print("\n🔹 热门市场新闻:")
    trending = news.trending()
    for i, item in enumerate(trending[:8], 1):  # 前8条
        print(f"\n   {i}. {item.get('title', 'N/A')}")
        if 'summary' in item:
            print(f"      📝 {item['summary'][:100]}...")
    
    # 3. 获取财经专题新闻
    print("\n🔹 财经要闻:")
    finance_news = news.finance()
    for i, item in enumerate(finance_news[:5], 1):
        print(f"   {i}. {item.get('title', 'N/A')}")
    
    # 4. 获取经济数据新闻
    print("\n🔹 经济要闻:")
    economy_news = news.economy()
    for i, item in enumerate(economy_news[:5], 1):
        print(f"   {i}. {item.get('title', 'N/A')}")

if __name__ == "__main__":
    get_us_market_news()
