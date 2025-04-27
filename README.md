# -# استيراد المكتبات اللازمة
from telegram import Update  # استيراد وظائف Telegram
from telegram.ext import Updater, CommandHandler, CallbackContext  # أدوات للتحكم في البوت

# دالة لبدء البوت (امر /start)
def start(update: Update, context: CallbackContext):
    update.message.reply_text("مرحبًا! أهلاً بك في بوت 'تفاعل معانا'. اكتب /help لرؤية الأوامر المتاحة.")

# دالة لعرض المساعدة (امر /help)
def help_command(update: Update, context: CallbackContext):
    update.message.reply_text("""
    الأوامر المتاحة:
    /start - بدء البوت
    /help - عرض المساعدة
    /challenge - بدء تحدي الكلمات
    """)

# دالة لتحدي الكلمات (امر /challenge)
def word_challenge(update: Update, context: CallbackContext):
    topics = ["الحيوانات", "الألوان", "المهن", "الأكلات"]  # مواضيع التحدي
    topic = random.choice(topics)  # اختيار موضوع عشوائي
    update.message.reply_text(f"موضوع التحدي: {topic}. اكتب أكبر عدد ممكن من الكلمات المرتبطة!")

# دالة رئيسية لتشغيل البوت
def main():
    # استخدم توكن البوت هنا (ضع توكنك الخاص)
    TOKEN = "YOUR_TELEGRAM_BOT_TOKEN"  # استبدل هذا بتوكن البوت الخاص بك
    updater = Updater(TOKEN)  # إعداد البوت باستخدام التوكن

    # إضافة أوامر البوت
    dispatcher = updater.dispatcher
    dispatcher.add_handler(CommandHandler("start", start))  # أمر /start
    dispatcher.add_handler(CommandHandler("help", help_command))  # أمر /help
    dispatcher.add_handler(CommandHandler("challenge", word_challenge))  # أمر /challenge

    # تشغيل البوت
    updater.start_polling()  # بدء استقبال الرسائل
    print("البوت يعمل الآن!")  # رسالة تأكيد
    updater.idle()  # إبقاء البوت قيد التشغيل

# تشغيل البرنامج
if __name__ == "__main__":
    main()
