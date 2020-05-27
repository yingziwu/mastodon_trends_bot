from dateutil import tz
from datetime import datetime

from environs import Env
from mastodon import Mastodon


def run():
    env = Env()
    env.read_env()
    access_token = env('ACCESS_TOKEN')
    api_base_url = env('API_BASE_URL')

    mastodon = Mastodon(access_token=access_token, api_base_url=api_base_url)
    trends = list(map(lambda x: x['name'], mastodon.trends(3)))

    CST = tz.gettz('Asia/Shanghai')
    d = datetime.now(CST)
    if trends:
        status = d.strftime('%Y年%m月%d日%H时') + '流行标签\n' + '#' + '\n#'.join(trends)
        mastodon.status_post(status, visibility='unlisted')


if __name__ == '__main__':
    run()
