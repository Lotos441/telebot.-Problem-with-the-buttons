# telebot.-Problem-with-the-buttons
help please. The " sup " command does not work, but it is completely correctly written. I suspect that the "info" command is interfering with it, since after I commented it out, the "sup" command started working

import telebot
import configuration
from telebot import types
from random import randint
from random import choice

bot = telebot.TeleBot(configuration.token)


@bot.message_handler(commands=['start'])
def start_message(message):
    bot.send_message(message.chat.id, 'привет, {}✋'.format(message.chat.first_name))
    bot.send_message(message.chat.id, 'все мои функции:\n/sup - сапёр\n/info - информация о вас')


# кнопки(информация профиля)
@bot.message_handler(commands=['info'])
def get_user_info(message):
    markup_inline_info = types.InlineKeyboardMarkup()
    item_yes = types.InlineKeyboardButton(text='да✅', callback_data='yes_for_info')
    item_no = types.InlineKeyboardButton(text='нет❌', callback_data='no_for_info')
    markup_inline_info.add(item_yes, item_no)
    bot.send_message(message.chat.id, ' хотите я скажу какую нибудь информацию о вашем аккаунте?',
                     reply_markup=markup_inline_info
                     )


@bot.callback_query_handler(func=lambda call: True)
def answer_for_info(call):
    if call.data == 'yes_for_info':
        markup_reply = types.ReplyKeyboardMarkup(resize_keyboard=True)
        item_id = types.KeyboardButton('мой id')
        item_username = types.KeyboardButton('мой ник')
        item_cansel = types.KeyboardButton('отмена')
        markup_reply.add(item_id, item_username, item_cansel)
        bot.send_message(call.message.chat.id, 'информация о вас',
                         reply_markup=markup_reply
                         )

        @bot.message_handler(content_types=['text'])
        def send_text(message):
            if message.text.lower() == 'мой id':
                bot.send_message(message.chat.id, f'твой ID: {message.from_user.id}')
            elif message.text.lower() == 'мой ник':
                bot.send_message(message.chat.id,
                                 f'твой никнейм: {message.from_user.first_name} {message.from_user.last_name}')
            elif message.text.lower() == 'мой ник':

    elif call.data == 'no_for_info':
        bot.send_message(call.message.chat.id, 'хорошо, отмена выдачи информации',
                         reply_markup=types.ReplyKeyboardRemove(), parse_mode='Markdown')


# игра в сапёр
@bot.message_handler(commands=['sup'])
def get_user_sup(message):
    markup_inline_for_sup = types.InlineKeyboardMarkup()
    item_yes_for_sup = types.InlineKeyboardButton(text='да', callback_data='yes_for_sup')
    item_no_for_sup = types.InlineKeyboardButton(text='нет', callback_data='no_for_sup')
    markup_inline_for_sup.add(item_yes_for_sup, item_no_for_sup)
    bot.send_message(message.chat.id, ' рискнешь разрезать правильный провод?',
                     reply_markup=markup_inline_for_sup
                     )


@bot.callback_query_handler(func=lambda call: True)
def answer_for_sup(call):
    if call.data == 'yes_for_sup':
        markup_reply_for_sup = types.ReplyKeyboardMarkup(resize_keyboard=True)
        item_1 = types.KeyboardButton('красный провод')
        item_2 = types.KeyboardButton('синий провод')
        item_3 = types.KeyboardButton('зеленый провод')
        item_4 = types.KeyboardButton('белый провод')
        item_5 = types.KeyboardButton('желтый провод')
        item_6 = types.KeyboardButton('черный провод')
        markup_reply_for_sup.add(item_1, item_2, item_3, item_4, item_5, item_6)
        bot.send_message(call.message.chat.id, 'игра рандомна! режь любой провод!',
                         reply_markup=markup_reply_for_sup
                         )

        @bot.message_handler(content_types=['text'])
        def send_text(message):
            bullet_in_gun = randint(1, 6)
            if message.text == 'красный провод':
                if bullet_in_gun == 1:
                    bot.send_message(message.chat.id, 'бах!')
                else:
                    bot.send_message(message.chat.id, 'тебе повезло!')
            if message.text == 'синий провод':
                if bullet_in_gun == 2:
                    bot.send_message(message.chat.id, 'бах!')
                else:
                    bot.send_message(message.chat.id, 'тебе повезло!')
            if message.text == 'зеленый провод':
                if bullet_in_gun == 3:
                    bot.send_message(message.chat.id, 'бах!')
                else:
                    bot.send_message(message.chat.id, 'тебе повезло!')
            if message.text == 'белый провод':
                if bullet_in_gun == 4:
                    bot.send_message(message.chat.id, 'бах!')
                else:
                    bot.send_message(message.chat.id, 'тебе повезло!')
            if message.text == 'желтый провод':
                if bullet_in_gun == 5:
                    bot.send_message(message.chat.id, 'бах!')
                else:
                    bot.send_message(message.chat.id, 'тебе повезло!')
            if message.text == 'черный провод':
                if bullet_in_gun == 6:
                    bot.send_message(message.chat.id, 'бах!')
                else:
                    bot.send_message(message.chat.id, 'тебе повезло!')
    elif call.data == 'no_for_sup':
        pass
