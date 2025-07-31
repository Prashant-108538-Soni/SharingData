class EventCardActionItem {
  final String title;
  final VoidCallback onTap;
  final bool isPrimary;

  EventCardActionItem({
    required this.title,
    required this.onTap,
    this.isPrimary = true,
  });
}




import 'package:flutter/material.dart';
import 'package:hdfc_flutter_widgets/common/secondary_button.dart';
import 'package:hdfc_flutter_widgets/common/tertiary_button.dart';

/// A row of buttons used at the bottom of the event card.
/// Takes a list of [EventCardActionItem] to render primary and secondary buttons.
class EventCardActions extends StatelessWidget {
  final List<EventCardActionItem> actions;

  const EventCardActions({super.key, required this.actions});

  @override
  Widget build(BuildContext context) {
    return Row(
      mainAxisAlignment: MainAxisAlignment.spaceBetween,
      children: actions
          .map((action) => Expanded(
                child: Padding(
                  padding: const EdgeInsets.only(right: 10),
                  child: action.isPrimary
                      ? SecondaryButton(title: action.title, onTap: action.onTap)
                      : TertiaryButton(
                          options: const [], // Will be populated if used as a menu
                          icon: const Icon(Icons.more_vert),
                          onSelect: (_) => action.onTap(),
                        ),
                ),
              ))
          .toList(),
    );
  }
}


CompactEventCard(
  menuOptions: ['Delete', 'Duplicate'],
  onTap: () => print("View Details"),
  onSelect: (option) => print("Selected: $option"),
  prefixIconPath: "assets/icons/phone.svg",
  suffixIconPath: "assets/icons/logo.svg",
  descriptionText: "Enabled",
  descriptionIconPath: "assets/icons/status.svg",
  amount: 950.50,
  paymentStatus: "Paid",
  paymentStatusBackgroundColor: Colors.green.shade100,
  paymentStatusTextColor: Colors.green.shade900,
  eventDate: "17 Sept",
  eventDateLabel: "PAID",
  eventName: "Mom's Phone Bill",
  backgroundColor: Colors.blue.shade100,
  accountDetails: "XXXX 4567",
  billType: "Mobile",
  subTitle: "Monthly Recharge",
  actionItems: [
    EventCardActionItem(
      title: "View Details",
      onTap: () => print("View Details tapped"),
      isPrimary: true,
    ),
    EventCardActionItem(
      title: "More",
      onTap: () => print("More tapped"),
      isPrimary: false,
    ),
  ],
);