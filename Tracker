import os
import time
import phonenumbers
from phonenumbers import carrier, geocoder, timezone, PhoneNumberType, PhoneMetadata
import pyfiglet
from datetime import datetime
from colorama import Fore, Style, init

init(autoreset=True)

def clear_screen():
    if os.name == 'nt':
        os.system('cls')
    else:
        os.system('clear')

clear_screen()

t = time.localtime(time.time())
localtime = time.asctime(t)
print("Waktu Lokal Saat Ini:", localtime)

ascii_art = pyfiglet.figlet_format("Sastra")
print(Fore.GREEN + ascii_art)

import requests

response = requests.get("https://api.ipify.org?format=json")
ip_data = response.json()

print("Alamat IP Publik Anda:", ip_data['ip'])

import socket

def get_local_ip():                                                                                                                                         # Mengambil hostname dari perangkat
    hostname = socket.gethostname()
    # Mendapatkan alamat IP lokal dari hostname
    local_ip = socket.gethostbyname(hostname)
    return local_ip

if __name__ == "__main__":
    local_ip = get_local_ip()
    print("Alamat IP Lokal Anda:", local_ip)

def get_number_type(number):
    number_type = phonenumbers.number_type(number)
    if number_type == PhoneNumberType.MOBILE:
        return "Ponsel"
    elif number_type == PhoneNumberType.FIXED_LINE:
        return "Telepon Tetap"
    elif number_type == PhoneNumberType.FIXED_LINE_OR_MOBILE:
        return "Telepon Tetap atau Ponsel"
    elif number_type == PhoneNumberType.TOLL_FREE:
        return "Bebas Pulsa"
    elif number_type == PhoneNumberType.PREMIUM_RATE:
        return "Nomor Premium"
    elif number_type == PhoneNumberType.VOIP:
        return "VoIP"
    elif number_type == PhoneNumberType.SHARED_COST:
        return "Biaya Bersama"
    elif number_type == PhoneNumberType.PAGER:
        return "Pager"
    elif number_type == PhoneNumberType.UAN:
        return "UAN"
    elif number_type == PhoneNumberType.VOICEMAIL:
        return "Voicemail"
    else:
        return "Tipe Tidak Diketahui"

try:
    current_time = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    print("Waktu Sekarang:", current_time)

    mobileNo = input("Masukkan nomor telepon (misal: +62822...): ")
    mobileNo = phonenumbers.parse(mobileNo, "ID")

    print(Fore.MAGENTA + "== Informasi Nomor ==")

    timezones = timezone.time_zones_for_number(mobileNo)
    print(Fore.MAGENTA + "Zona Waktu:", timezones)

    provider = carrier.name_for_number(mobileNo, "id")
    print(Fore.MAGENTA + "Operator:", provider)

    region = geocoder.description_for_number(mobileNo, "id")
    print(Fore.MAGENTA + "Lokasi:", region)

    is_valid = phonenumbers.is_valid_number(mobileNo)
    print(Fore.MAGENTA + "Nomor Valid:", is_valid)

    is_possible = phonenumbers.is_possible_number(mobileNo)
    print(Fore.MAGENTA + "Nomor Mungkin Valid:", is_possible)

    international_format = phonenumbers.format_number(mobileNo, phonenumbers.PhoneNumberFormat.INTERNATIONAL)
    print(Fore.MAGENTA + "Format Internasional:", international_format)

    mobile_format = phonenumbers.format_number(mobileNo, phonenumbers.PhoneNumberFormat.NATIONAL)
    print(Fore.MAGENTA + "Format Nasional:", mobile_format)

    e164_format = phonenumbers.format_number(mobileNo, phonenumbers.PhoneNumberFormat.E164)
    print(Fore.MAGENTA + "Format E.164:", e164_format)

    country_code = mobileNo.country_code
    print(Fore.MAGENTA + "Kode Negara:", country_code)

    local_number = mobileNo.national_number
    print(Fore.MAGENTA + "Nomor Lokal:", local_number)

    number_length = len(str(local_number))
    print(Fore.MAGENTA + "Panjang Nomor Telepon:", number_length)

    number_type = get_number_type(mobileNo)
    print(Fore.MAGENTA + "Tipe Nomor:", number_type)

    print(Fore.MAGENTA + "== Informasi Tambahan ==")

    if number_type == "Nomor Premium":
        print(Fore.MAGENTA + "Peringatan: Ini adalah nomor premium, mungkin dikenakan biaya tambahan.")
    else:
        print(Fore.MAGENTA + "Ini bukan nomor premium.")

    if timezones:
        print(Fore.MAGENTA + "Nomor ini terkait dengan zona waktu:", ", ".join(timezones))
    else:
        print(Fore.MAGENTA + "Tidak ada zona waktu yang terkait dengan nomor ini.")

    is_possible_as_mobile = phonenumbers.is_possible_number_for_type(mobileNo, PhoneNumberType.MOBILE)
    print(Fore.MAGENTA + "Mungkin sebagai Nomor Ponsel:", is_possible_as_mobile)

    has_extension = mobileNo.extension is not None
    print(Fore.MAGENTA + "Memiliki Extension:", has_extension)

    optimal_format = phonenumbers.format_by_pattern(mobileNo, phonenumbers.PhoneNumberFormat.INTERNATIONAL, [])
    print(Fore.MAGENTA + "Format Optimal:", optimal_format)

    is_valid_for_region = phonenumbers.is_valid_number_for_region(mobileNo, "ID")
    print(Fore.MAGENTA + "Valid untuk Region Indonesia:", is_valid_for_region)

    metadata = PhoneMetadata.load_all()
    print(Fore.MAGENTA + "Metadata Nomor Telepon Dimuat")

    print(Fore.MAGENTA + "Status Nomor: ")

    print(Fore.MAGENTA + "INI ADALAH NOMER TELPON")

except phonenumbers.NumberParseException as e:
    print(f"Kesalahan dalam memproses nomor: {e}")
